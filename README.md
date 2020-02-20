This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.<br />
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br />
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.<br />
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.<br />
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br />
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: https://facebook.github.io/create-react-app/docs/code-splitting

### Analyzing the Bundle Size

This section has moved here: https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size

### Making a Progressive Web App

This section has moved here: https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app

### Advanced Configuration

This section has moved here: https://facebook.github.io/create-react-app/docs/advanced-configuration

### Deployment

This section has moved here: https://facebook.github.io/create-react-app/docs/deployment

### `npm run build` fails to minify

This section has moved here: https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify

### React --> Azure Guideline

** Prepare local react app reposiotory in VS code**

1) npm init react-app <appname>
2) cd <appname>
3) add following lines to package.json:
    "engines": {
        "node": "10.0"
    }
4) npm install
5) npm run build
6) git init
7) git add .
8) git commit -m "first commit"
9) git remote add azure <git_clone_url>
10) git push -u azure master
11) touch web.config 
12) add following lines in web.config
    <?xml version="1.0"?>
    <configuration>
        <system.webServer>
            <rewrite>
                <rules>
                    <rule name="React Routes" stopProcessing="true">
                        <match url=".*" />
                        <conditions logicalGrouping="MatchAll">
                            <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
                            <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />
                            <add input="{REQUEST_URI}" pattern="^/(api)" negate="true" />
                        </conditions>
                        <action type="Rewrite" url="/" />
                    </rule>
                </rules>
            </rewrite>
        </system.webServer>
    </configuration>
13) install following extensions: XML Tools, Azure Tools
14) in web.config, press SHIFT+ALT+F to format xml file
15) npm run build

** Prepare Azure Environment ** 
1) Create new resource -> WebApp
2) Choose subsciption, resource group, name, publish (code), Rutime stack (node 10.0), Operating system (Windows), Region
3) Next -> Allow AppInsights --> Next --> Create
4) Wati till the app starts => Go to resource => Deployment center
5) Source Control: Github (sign in if needed)
6) Build provider: Kudu (App Service build service)
7) Configure to your <git_clone_url>
