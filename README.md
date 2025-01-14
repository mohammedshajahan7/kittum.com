# ml-xn-kittum

ലിങ്ക് ഉണ്ടാക്കേണ്ട രീതി: `ഡാഷ്-വെച്ചോ-അണ്ടർസ്കോർ_വെച്ചോ-വേർതിരിച്ച-വാക്കുകൾ.കിട്ടും.com`.

എല്ലാത്തിന്റേം അവസാനം ഒരു `.കിട്ടും.com` വെക്ക്. 😌

Format: <some-words-separated-by-dash-or_underscore>.കിട്ടും.com

Words should be separated by dash `-` or underscore `_`.

* https://നോക്കി-ഇരുന്നോ-ഇപ്പോ.കിട്ടും.com
* https://ബിരിയാണി-ഇപ്പോ.കിട്ടും.com
* https://കിട്ടും.കിട്ടും.com
* https://ബിരിയാണി-എപ്പോ.കിട്ടും.com

## പ്രത്യേക താളുകൾ

URL അനുസരിച്ച് താളിന്റെ രൂപം മാറ്റാൻ കഴിയും. ഇതിനായി `src/pages/index.json` കാണുക. RegEx വെച്ചാണ് ഇത് സാധ്യമാക്കുന്നത്, താളിന്റെ തലക്കെട്ടും, ഉപതലക്കെട്ടും ഇതുവഴി മാറ്റാവുന്നതാണ്.

ഉദാ: URL ന്റെ അവസാനം `എപ്പോ`, `എപ്പൊ` അഥവാ `എപ്പോൾ` എന്ന് വരുമ്പോൾ താളിന്റെ തലക്കെട്ട് "നോക്കി ഇരുന്നോ ഇപ്പോ കിട്ടും" എന്നാക്കാൻ വേണ്ടിയുള്ള ക്രമീകരണം:

```json
{
  "regex": "^(.*?)(എപ്പോ|എപ്പൊ|എപ്പോൾ)$",
  "title": "നോക്കി ഇരുന്നോ ഇപ്പോ കിട്ടും",
  "subtitle": ""
}
```

## Development

The frontend is written in Vue and backend in Go. We use Go for pre-rendering `<title>`, `<meta>` tags. Read [this blog post](https://subinsb.com/run-js-code-from-go-with-chrome-v8-engine/) for more.

After cloning the repo, do these one-by-one to start the server :

```bash
pnpm build && pnpm build:utils
go run .
```

ഇനി പണി തുടങ്ങിക്കോളീൻ.

### Deployment

Host on any Linux server.

```
pnpm build && pnpm build:utils
go build .
./restart.sh
```

An nginx config example is in repo. Note that LetsEncrypt allow single-level wildcard subdomains only (`*.example.com`). It doesn't give infinite wildcard subdomains (`*.*.example.com`). This is why the URL format recommends to use `-` as splitter instead of dot(`.`).
