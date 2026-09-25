# Onshape REST API cheat sheet

Items marked [verify] came from partial docs — confirm with a GET or the API Explorer (https://cad.onshape.com/glassworks/explorer/) before relying on them.

## Anatomy
- Base: `https://cad.onshape.com/api/v{N}/…` (version number in path).
- Browser URL `…/documents/{did}/w/{wid}/e/{eid}` ↔ API path `/{area}/d/{did}/{w|v|m}/{wvmid}/e/{eid}`. IDs 24 chars.
- w = workspace (writable), v = version, m = microversion (immutable). POST only to w.
- Rate limit header `X-Rate-Limit-Remaining`.

## Auth
- API keys (My Account → Developer). Basic auth `base64(access:secret)` for local dev; HMAC-SHA256 signed requests (`Date`, `On-Nonce`, `Authorization: On <access>:HmacSHA256:<sig>`) for robustness; OAuth2 for App Store apps.
- Read `ONSHAPE_ACCESS_KEY` / `ONSHAPE_SECRET_KEY` from env.

## Part Studio features
- List/add: `GET|POST /partstudios/d/{did}/{wvm}/{wvmid}/e/{eid}/features`
- Update: `POST /partstudios/d/{did}/w/{wid}/e/{eid}/features/featureid/{fid}`
- Batch update: `POST …/features/updates` [verify]
- Delete: `DELETE …/features/featureid/{fid}`
- Body: `{"feature": {"btType":"BTMFeature-134","featureType":"extrude","name":"Tube Extrude","parameters":[…]}}` (wrapper BTFeatureDefinitionCall-1406).
- Params: `BTMParameterQuantity-147 {parameterId, expression}`, `BTMParameterEnum-145 {parameterId, enumName, value}`, `BTMParameterBoolean-144`, `BTMParameterQueryList-148 {queries:[BTMIndividualQuery-138 {deterministicIds|queryString}] }`, sketch regions `BTMIndividualSketchRegionQuery-140 {featureId}`.
- Extrude ids: `bodyType`=SOLID, `operationType`=NEW|ADD|REMOVE|INTERSECT, `entities`, `endBound`=BLIND|UP_TO_FACE|…, `depth`.
- Response: `featureState` per feature (OK / ERROR / INACTIVE), `sourceMicroversion`, `serializationVersion`.

## Sketches
- `BTMSketch-151`, `featureType:"newSketch"`, `sketchPlane` query e.g. `qCreatedBy(makeId("Front"), EntityType.FACE);`
- Entities: `BTMSketchCurveSegment-155` + `BTCurveGeometryLine-117`; `BTMSketchCurve-4` + `BTCurveGeometryCircle-115` (radius, xCenter, yCenter in **meters**), each with `entityId`.
- Constraints: `BTMSketchConstraint-2` with `constraintType` (COINCIDENT, HORIZONTAL, DISTANCE, DIAMETER, EQUAL, …) and parameters referencing entity ids [verify exact param ids by GET of a hand-made sketch].

## FeatureScript evaluation
`POST /api/v6/partstudios/d/{did}/w/{wid}/e/{eid}/featurescript` body `{"script":"function(context is Context, queries){ return …; }"}` — lambdas only. Use for deterministic IDs (`transientQueriesToStrings(evaluateQuery(context, q))`), measurements, part counts.

## Custom features
Added like any feature; `namespace` encodes the Feature Studio doc/version/element. Copy it from a GET of a manually inserted instance. Feature specs: `GET /partstudios/…/featurespecs` [verify].

## Variables & configurations
- Variables tables: `/variables/d/{did}/{wvm}/{wvmid}/e/{eid}/variables` [verify]. Or add `variable` features in a part studio.
- Configuration: `GET|POST /elements/d/{did}/wvm/{wvmid}/e/{eid}/configuration`; encode with `POST /elements/d/{did}/e/{eid}/configurationencodings` → `configuration=…` query string.

## Assemblies
- Definition: `GET /assemblies/d/{did}/{wvm}/{wvmid}/e/{eid}` (includeMateFeatures, includeMateConnectors).
- Insert: `POST /assemblies/d/{did}/w/{wid}/e/{eid}/instances` {documentId, elementId, partId | isWholePartStudio, versionId, configuration}.
- Transforms: `POST …/modify` (4×4 row-major absolute).
- Mates: `POST /assemblies/…/features` with `BTMMateConnector-66` (originType ON_ENTITY, originQuery BTMInferenceQueryWithOccurrence-1083) and `BTMMate-64` (mateType FASTENED|REVOLUTE|SLIDER|CYLINDRICAL|PIN_SLOT|PLANAR|BALL|PARALLEL, mateConnectorsQuery with two BTMFeatureQueryWithOccurrence-157).

## Versions
Create a version before cross-document inserts/derives (documents API `POST /documents/d/{did}/versions` [verify]).

## Export
`POST /partstudios/…/export/step|stl` or `/assemblies/…/export/step` → poll `GET /translations/{id}` until DONE → `GET /blobelements/d/{did}/{wv}/{wvid}/e/{resultElementId}`.
