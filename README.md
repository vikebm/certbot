# Guide to generate free SSL certificates

 This is a simple guide whith examples to generate free SSL certificates in ubuntu with node.js and letsencrypt
 
 
#### Install cerbot
```bash
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install certbot
```

*Note: To generate the certificates for the specified domain you must have port 80 free.*

#### Generate certificates
```bash
certbot certonly --auto
```

*Note: For certificates to be generated automatically; dns should point to the server where our application will run*

In this route the certificates will be generated
**/etc/letsencrypt/live/**

## Usage Examples
#### Example #1
```
import https from "https";
import express from "express";
import fs from "fs;

const app = express();
const privateKey = fs.readFileSync(
  path.resolve(__dirname, "../certificates/ssl/privkey1.pem")
);
const certificate = fs.readFileSync(
  path.resolve(__dirname, "../certificates/ssl/fullchain1.pem")
);
const ca = fs.readFileSync(
  path.resolve(__dirname, "../certificates/ssl/chain1.pem")
);

const credentials = { key: privateKey, cert: certificate, ca: ca };
const httpsServer = https.createServer(credentials, app);
httpsServer.listen(443);
```

#### Example #2
Rename the generated files **cert1.pem** and **privkey.pem** to **cert1.crt** and **privkey.key** respectively.
```
import https from "https";
import express from "express";
import fs from "fs;

const app = express();
const certificate = fs.readFileSync('../certificates/ssl/cert1.crt', 'utf8');
const privateKey = fs.readFileSync('../certificates/ssl/privkey.key', 'utf8');
const credentials = { key: privateKey, cert: certificate };
const httpsServer = https.createServer(credentials, app);

httpsServer.listen(443);
```



