# step-functions-bluegreen-deploy-demo

Demo project to illustrate how to implement blue-green deployment with Step Functions so you don't break existing executions.

For more details, check out [this blog post](https://theburningmonk.com/2019/08/how-to-do-blue-green-deployment-for-step-functions/).

To try this out yourself:

1. run `npm install` to install the dependencies

2. switch to the `v1` branch and run `npm run sls -- deploy`

3. once deployed, trigger a new execution by running `npm run sls -- invoke stepf --name myStateMachine --data '{"foo":"bar"}'`. You can inspect the Step Functions console to see that the execution is running and is in the `Wait` state for 5 mins.

4. switch to the `v2` branch and run `npm run sls -- deploy`

5. once deployed, trigger another execution by running `npm run sls -- invoke stepf --name myStateMachine --data '{"foo":"bar"}'`. This time, the new state machine would complete right away.

The first execution would transition to its `Hello` state after 5 mins and it will still complete successfully (even though we have changed the output from the `hello` function as well as the state machine definition).
