# Next 12.x.y

## EDGE-PAGES-12.3.4

``` bash
edge-pages-12-3-4 git:(main) npm install

> edge-pages-12-3-4@0.1.0 postinstall
> patch-package

patch-package 6.5.1
Applying patches...
No patch files found

added 267 packages, and audited 268 packages in 19s

93 packages are looking for funding
  run `npm fund` for details

3 moderate severity vulnerabilities

To address issues that do not require attention, run:
  npm audit fix

To address all issues (including breaking changes), run:
  npm audit fix --force

Run `npm audit` for details.
➜  edge-pages-12-3-4 git:(main) azion link 
? Do you want to link /Users/gabriel.franca/Desktop/next12-tests/jamstack-playground/Nextjs/Azion/edge-pages-12-3-4 to Azion? Yes
? (Hit enter to accept the suggested name in parenthesis) Your application's name:  insightful_enchantment

Getting modes available (Some dependencies may need to be installed)
? Choose a preset and mode: Next (Compute)
Template successfully fetched and configured

? Do you want to start a local development server? Yes
? Do you want to install project dependencies? This may be required to start local development server Yes
? Choose a package manager: npm

> edge-pages-12-3-4@0.1.0 postinstall
> patch-package

patch-package 6.5.1
Applying patches...
No patch files found

up to date, audited 268 packages in 3s

93 packages are looking for funding
  run `npm fund` for details

3 moderate severity vulnerabilities

To address issues that do not require attention, run:
  npm audit fix

To address all issues (including breaking changes), run:
  npm audit fix --force

Run `npm audit` for details.
Building your edge application. This process may take a few minutes
Running build step command:

$ npx --yes edge-functions@1.7.0 build --preset next --mode compute
[Vulcan] [Pre Build] › ℹ  info      Starting prebuild...
[Vulcan] [Pre Build] › ℹ  info      Starting Next.js build process ...
[Vulcan] [Pre Build] › ℹ  info      Detected Next.js version: ^12.3.4
[Vulcan] [Pre Build] › ℹ  info      Checking vercel config file ...
[Vulcan] [Pre Build] › ℹ  info      Running Next.js vercel build ...
Vercel CLI 32.2.1
Warning: When using Next.js, it is recommended to place JavaScript Functions inside of the `pages/api` (provided by Next.js) directory instead of `api` (provided by Vercel). Other languages (Python, Go, etc) should still go in the `api` directory. Learn More: https://nextjs.org/docs/api-routes/introduction
Installing dependencies...

> edge-pages-12-3-4@0.1.0 postinstall
> patch-package

patch-package 6.5.1
Applying patches...
No patch files found

up to date in 3s

93 packages are looking for funding
  run `npm fund` for details
Detected Next.js version: 12.3.4
Detected `package-lock.json` generated by npm 7+
Running "npm run build"

> edge-pages-12-3-4@0.1.0 build
> next build

warn  - You have enabled experimental feature (runtime) in next.config.js.
warn  - Experimental features are not covered by semver, and may cause unexpected or broken application behavior. Use at your own risk.

Attention: Next.js now collects completely anonymous telemetry regarding usage.
This information is used to shape Next.js' roadmap and prioritize features.
You can learn more, including how to opt-out if you'd not like to participate in this anonymous program, by visiting the following URL:
https://nextjs.org/telemetry


./pages/api/hello.js
7:1  Warning: Unexpected default export of anonymous function  import/no-anonymous-default-export

info  - Need to disable some ESLint rules? Learn more here: https://nextjs.org/docs/basic-features/eslint#disabling-rules
info  - Linting and checking validity of types  
warn  - You are using an experimental edge runtime, the API might change.
warn  - You are using the experimental Edge Runtime with `experimental.runtime`.
info  - Creating an optimized production build  
info  - Compiled successfully
"getStaticProps" is not yet supported fully with "experimental-edge", detected on /[...catSlug]
"getStaticProps" is not yet supported fully with "experimental-edge", detected on /[prodSlug]/x
info  - Collecting page data  
info  - Generating static pages (2/2)
info  - Finalizing page optimization  

Route (pages)                              Size     First Load JS
┌ ℇ /                                      5.51 kB        84.2 kB
├   └ css/84ac3d293c1a5243.css             729 B
├   /_app                                  0 B            78.7 kB
├ ℇ /[...catSlug]                          363 B            79 kB
├ ℇ /[prodSlug]/x                          365 B            79 kB
├ ○ /404                                   182 B          78.9 kB
├ ℇ /api/hello                             0 B            78.7 kB
└ ℇ /ssr                                   367 B            79 kB
+ First Load JS shared by all              78.9 kB
  ├ chunks/framework-7751730b10fa0f74.js   45.5 kB
  ├ chunks/main-c3533e82930cc74b.js        31.9 kB
  ├ chunks/pages/_app-1a336683ff51f334.js  497 B
  ├ chunks/webpack-8fa1640cc84ba8fe.js     750 B
  └ css/ab44ce7add5c3d11.css               247 B

ƒ Middleware                               21.1 kB

ℇ  (Streaming)  server-side renders with streaming (uses React 18 SSR streaming or Server Components)
○  (Static)     automatically rendered as static HTML (uses no initial props)

Traced Next.js server files in: 1.840s
Created all serverless functions in: 534.08ms
Collected static files (public/, static/, .next/static): 7.402ms
Warning: Node.js functions are compiled from ESM to CommonJS. If this is not intended, add "type": "module" to your package.json file.
Compiling "middleware.js" from ESM to CommonJS...
✅  Build Completed in .vercel/output [35s]
[Vulcan] [Pre Build] › ℹ  info      Cleaning files ...
[Vulcan] [Pre Build] › ℹ  info      Running default Next.js build ...
[Vulcan] [Pre Build] › ✖  error     Not implemented build!
Error: Error executing Vulcan: Failed to run the build command. Verify if the command is correct and check the output above for more details. Run the 'azion build' command again or contact Azion's support
➜  edge-pages-12-3-4 git:(main) node -v
v18.18.2
➜  edge-pages-12-3-4 git:(main) azion -v
Azion CLI 1.4.0
```

Changed version to `12.3.1`

```
edge-pages-12-3-4 git:(main) ✗ azion link
? Do you want to link /Users/gabriel.franca/Desktop/next12-tests/jamstack-playground/Nextjs/Azion/edge-pages-12-3-4 to Azion? Yes
? This project was already configured. Do you want to override the previous configuration? Yes
? (Hit enter to accept the suggested name in parenthesis) Your application's name:  enthusiastic_pangolin

Getting modes available (Some dependencies may need to be installed)
? Choose a preset and mode: Next (Compute)
Template successfully fetched and configured

? Do you want to start a local development server? Yes
? Do you want to install project dependencies? This may be required to start local development server Yes
? Choose a package manager: npm

> edge-pages-12-3-4@0.1.0 postinstall
> patch-package

patch-package 6.5.1
Applying patches...
No patch files found

up to date, audited 69 packages in 2s

10 packages are looking for funding
  run `npm fund` for details

2 moderate severity vulnerabilities

To address all issues (including breaking changes), run:
  npm audit fix --force

Run `npm audit` for details.
Building your edge application. This process may take a few minutes
Running build step command:

$ npx --yes edge-functions@1.7.0 build --preset next --mode compute
[Vulcan] [Pre Build] › ℹ  info      Starting prebuild...
[Vulcan] [Pre Build] › ℹ  info      Starting Next.js build process ...
[Vulcan] [Pre Build] › ℹ  info      Detected Next.js version: 12.3.1
[Vulcan] [Pre Build] › ℹ  info      Checking vercel config file ...
[Vulcan] [Pre Build] › ℹ  info      Running Next.js vercel build ...
Vercel CLI 32.2.1
Warning: When using Next.js, it is recommended to place JavaScript Functions inside of the `pages/api` (provided by Next.js) directory instead of `api` (provided by Vercel). Other languages (Python, Go, etc) should still go in the `api` directory. Learn More: https://nextjs.org/docs/api-routes/introduction
WARNING: You should not upload the `.next` directory.
Installing dependencies...

> edge-pages-12-3-4@0.1.0 postinstall
> patch-package

patch-package 6.5.1
Applying patches...
No patch files found

up to date in 780ms

10 packages are looking for funding
  run `npm fund` for details
Detected Next.js version: 12.3.1
Detected `package-lock.json` generated by npm 7+
Running "npm run build"

> edge-pages-12-3-4@0.1.0 build
> next build

warn  - You have enabled experimental feature (runtime) in next.config.js.
warn  - Experimental features are not covered by semver, and may cause unexpected or broken application behavior. Use at your own risk.

info  - Linting and checking validity of types .error - ESLint: Failed to load config "next/core-web-vitals" to extend from. Referenced from: /Users/gabriel.franca/Desktop/next12-tests/jamstack-playground/Nextjs/Azion/edge-pages-12-3-4/.eslintrc.json
info  - Linting and checking validity of types  
warn  - You are using an experimental edge runtime, the API might change.
warn  - You are using the experimental Edge Runtime with `experimental.runtime`.
info  - Creating an optimized production build  
info  - Compiled successfully
"getStaticProps" is not yet supported fully with "experimental-edge", detected on /[prodSlug]/x
"getStaticProps" is not yet supported fully with "experimental-edge", detected on /[...catSlug]
info  - Collecting page data  
info  - Generating static pages (2/2)
info  - Finalizing page optimization  

Route (pages)                              Size     First Load JS
┌ ℇ /                                      5.51 kB        84.2 kB
├   └ css/84ac3d293c1a5243.css             729 B
├   /_app                                  0 B            78.7 kB
├ ℇ /[...catSlug]                          363 B            79 kB
├ ℇ /[prodSlug]/x                          365 B            79 kB
├ ○ /404                                   182 B          78.9 kB
├ ℇ /api/hello                             0 B            78.7 kB
└ ℇ /ssr                                   367 B            79 kB
+ First Load JS shared by all              78.9 kB
  ├ chunks/framework-7751730b10fa0f74.js   45.5 kB
  ├ chunks/main-1c975056d500063c.js        31.9 kB
  ├ chunks/pages/_app-1a336683ff51f334.js  497 B
  ├ chunks/webpack-8fa1640cc84ba8fe.js     750 B
  └ css/ab44ce7add5c3d11.css               247 B

ƒ Middleware                               21.1 kB

ℇ  (Streaming)  server-side renders with streaming (uses React 18 SSR streaming or Server Components)
○  (Static)     automatically rendered as static HTML (uses no initial props)

Traced Next.js server files in: 1.064s
Created all serverless functions in: 308.891ms
Collected static files (public/, static/, .next/static): 7.971ms
Warning: Node.js functions are compiled from ESM to CommonJS. If this is not intended, add "type": "module" to your package.json file.
Compiling "middleware.js" from ESM to CommonJS...
✅  Build Completed in .vercel/output [23s]
[Vulcan] [Pre Build] › ℹ  info      Cleaning files ...
[Vulcan] [Pre Build] › ℹ  info      Running default Next.js build ...
[Vulcan] [Pre Build] › ✖  error     Not implemented build!
Error: Error executing Vulcan: Failed to run the build command. Verify if the command is correct and check the output above for more details. Run the 'azion build' command again or contact Azion's support
```