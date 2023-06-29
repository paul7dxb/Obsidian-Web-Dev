# Lambda Imports

## Cannot import package
- run `npm install` from within the lambda folder that contains a `package.json` file

## Layer cannot find /opt/layer

- Name of lambda file imported must be the same as the lambda file in the CF template
- e.g `const db_access = require('/opt/db-read');`
- Would have the layer folder structure:

![[CDK_Lambda_Layer_TS.png]]
