## Trello Power-Up Notes

### How do I get started developing?

1. Create a new Power-Up on Trello from the [Admin Page](https://trello.com/power-ups/admin)
2. Enable the capabilities in the 'Capabilities' section that you'd like to enable (e.g. all)
3. Create a `.env` file based on the `.env.example` file and change the following values:
   - POWERUP_NAME - The name of your new Power-Up
   - POWERUP_ID - The Power-Up ID, retrieved from the URL of the Power-Up configuration page that you landed on in Step 1 (e.g. https://trello.com/power-ups/**abc001**/edit)
   - POWERUP_APP_KEY - Get your App Key from Trello on [this page](https://trello.com/app-key)
4. Install dependencies with `yarn install` or `npm install`
5. Run the Power-Up in development mode with `yarn dev` or `npm run dev`
6. You will be provided a URL endpoint like https://ddsdsdsds.ngrok.io/ - this should be pasted in the 'Iframe Connector URL' field on the Power-Up configuration page.
7. Open a Trello Board and add the Power-Up you created in Step 1 from the 'Custom' section.
8. You now have a Power-Up running and should see any changes you make to the React front-end are automatically reflected in the browser!

### Project Structure

Find out how the project is structured and what the files do!

- `src/`
  - `capabilities.ts` - This is the Power-Up descriptor and describes which capabilities are implemented - e.g. Card Buttons. Any UI elements that are rendered by Trello itself are contained in this file.
  - `router.ts` - This file contains the React-Router code, which is used to render the correct React components for their corresponding URL's.
  - `server.ts` - A basic script to serve the pages using Node.js (not recommended, as you can use the static files in /dist to save overhead/money). Call it with `yarn start`
  - `dev-watch.ts` - A script that runs a self-contained development environment. Call it with `yarn watch`
  - `dev-server.ts` - Runs the 'server.ts' file after reading in any environmental variables from your `.env` file. Call it with `yarn start:dev`.
  - `api/` - Contains any abstracted API functions that are used by the App (e.g. openPopup, getNotesForCard).
  - `<capability>/` - Each capability that includes a React Front-End has its own folder components and styles.
  - `types/` - Contains Typings for the Power-Up and for Trello.
- `static/` - Contains static files that should be included in the Power-Up distribution (e.g. Favicon)
- `templates/` - Contains handlebars templates that are used by Webpack to build matching \*.html files for each extension point.
- `.env.example` - An example environmental variables file that can be used during development (make a copy of this file, name it `.env` and modify it according to your requirements.
- `package.json` - This file describes the dependencies used by the Power-Up, basic information and scripts.
- `webpack.config.ts` - The Webpack file describes 'how the Power-Up should be compiled' and handles transpiling, file generation and also contains the configuration for running the Webpack Dev Server.
  - Run `yarn build` to build the app in production mode.
  - Run `yarn build:dev` to build and watch for changes in development mode.
