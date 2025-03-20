# Reproducing authentication retry failure inside banno widget
To make it possible for users to retry authentication (including inside the widget on the dashboard) we placed a redirect URI hyperlink, which triggers user authentication. But when trying to authenticate by this hyperlink, the banno server gives a response with the 400 code.

## How to Run
1. Install dependencies `npm install`
1. Rename `config-EXAMPLE.js` to `config.js`
1. Add `client_id`, `client_secret`, and `environment` to the config file
1. Ensure the port set in `config.js` is available on your system (8080 by default)
1. Configure external app in Banno People with correct redirect uri
1. Add the plugin to the user dashboard
1. Run the app with `npm run start`

## How to Reproduce the issue
1. Open Banno user dashdoard
1. Click "Try authentication again" -> Failure with 400 response code
1. Click card (widget) action button
1. Wait for the new page to load (expanded-view)
1. Click "Try authentication again" -> Succesfull authentication retry

## Authentication proccess scenario
- The user is already authenticated in Banno and is on the dashboard.
- Further, if the user’s authentication fails in the external application, an “Try again” hyperlink appears in the widget.
- Clicking the link leads to the same url that is specified in the developer environment in the widget settings. This is the endpoint for SSO user authentication in the external application.
- Next, the banno server gives a response with code 400.

## Important details
- This issue occurs inside of the Banno widget on the dashboard (card-face-view),
- and doesn't occur outside of the Banno widget after card (widget) action button clicking (expanded-view).
