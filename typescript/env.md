# when import "dotenv/config";
the dotenv refers .env file inside the cwd
not repo root
so run file from where .env file is

if still want in subfolder, follow this
replace the import "dotenv/config" with
```bash
import * as dotenv from "dotenv";
import * as path from "path";

// This tells dotenv to go up two directories from the current file to find .env
dotenv.config({ path: path.resolve(__dirname, "../../.env") });
```