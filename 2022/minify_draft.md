# Minification

```bash
npm install -g esbuild

esbuild --bundle src/index.ts --outdir="./dist" --format=esm --sourcemap --minify --mangle-props=^_ --reserve-props=^__
```

```bash
npm install -g google-closure-compiler

google-closure-compiler --js=bootstrap.js --js_output_file=bootstrap.min.js --rewrite_polyfills=false --language_out ECMASCRIPT_2015 --warning_level=QUIET
```
