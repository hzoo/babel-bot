# babel-bot

<p align="center">
    <img src="babel-bot.png" height="300px"/>
</p>

A bot used by the [`Babel`](https://github.com/babel/babel) team to automate common tasks in GitHub repositories. Allows taking action on events triggered from the GitHub webhooks API.

The bot is build as an [AWS Lambda](https://aws.amazon.com/lambda/) function, using [AWS API Gateway](https://aws.amazon.com/api-gateway/) to map the requests to an endpoint.

## Features

- Create a new comment on newly opened issues
- Reply to issue with canned response when `Needs Info` label is added
- Add labels to new PRs identifying which packages from the monorepo have been touched

## Future Bot Ideas

- https://github.com/babel/notes/issues/8

## Adding a New Event

1. Look at the list of [GitHub webhook events](https://developer.github.com/webhooks/#events) to determine which your rule should respond to.
2. Find (or create) a folder under `src/handlers` with the name matching the name of the GitHub `event`
3. Create a new JS file under the directory, with the name matching the `action` you want your code to be triggered for
4. Export a default function that accepts 1 argument, which will be the payload from GitHub each time the event is triggered.

Examples of existing event rules can be found in `src/handlers`.

## Setting up AWS Lamdba/API Gateway as a Test Environment

Visit [the guide](AWS_SETUP.md) for detailed instructions.

## Unit-Testing

Examples of how to test a handler can be seen in `src/handlers/issues/__tests__`.

## Deploying a New Version to AWS Lamdba

This process is currently manual, but will likely be automated in the future.

1. Run `yarn run package`, which will create `function.zip` in the root of the repository
2. Login to the AWS console, and find the function in the Lambda dashboard, under `Functions`
3. Click the `Upload` button under the `Code` tab (`Code Entry Type` should be set to `Upload a .ZIP file`)
4. Click `Save`
