In this exercise, you will return to the AWS Cloud9 instance and run the local build for the project. The local build contains linting, which is a static analysis of the code and unit tests. Imagine the development team of this project would use the local build scripts to verify their code before doing a commit. Next, you will run an integration test. The integration test finds the API Gateway WebSocket endpoint and simulates a player completing a game. This is the type of test we are using to verify our deployments to a staging environment. But, as always, there is plenty of room for your own experimentation. So think about what could be other implementations for validating that.
# __
Once you are happy with the tests, if the code looks good, you will add a simple feature to the application by making changes to the code. For user experience purposes, project managers realize that players are happier with big scores. So they asked if the game can give 20 points for each correct answer instead of the original 10 points. Next, you will make changes to the code and run the local build. The unit's tests will fail. This is expected because a functionality of scoring was changed, and the initial test is checking scores as being incremented by 10. When you fix up the unit tests and rerun the build, you will see success, which is always a good indicator.