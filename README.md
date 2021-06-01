# IOUBlockchain - A mini full-stack CorDapp development product

## Usage

### Deploy the app
1. Deploy nodes: `./gradlew deployNodes`
2. Run REST server: `.gradlew runServer`
3. Go to the website: localhost:8080

### Interact with the website
1. Register: user needs to register to use the website
2. Login: login to do operations
3. Issue IOUs: click on `Issue new Loans` to issue ious, you need to know the account name of the counterpart
4. Pay IOUs: as a borrower, you can pay back the money you owe. Click `Pay` and you will be prompted with payment amount.
5. Retire IOUs: when the amount on a IOU becomes 0, you can retire it by clicking the `Retire` button.


##TODO
* add markups
* exception handling
* "Blame" feature
* handle routing conflict
