# Kanban and onedev



## running as quickly as possible

> Following instructions at https://code.onedev.io/projects/162/blob/main/pages/quickstart.md

* First launch onedev in one docker container :

```bash
mkdir onedevtry/
cd onedevtry/

docker run --tty --rm -v /var/run/docker.sock:/var/run/docker.sock -v $(pwd)/onedev:/opt/onedev -p 6610:6610 -p 6611:6611 1dev/server

```

* Now you have access to :

![first access to onedev ui](./documentation/hugo/static/images/onedev/quickstart/onedev_ui_first_access.png)

* And you go through first setup steps :

![first setup steps 1](./documentation/hugo/static/images/onedev/quickstart/edev_ui_first_access_step1.png)

![first setup steps 2](./documentation/hugo/static/images/onedev/quickstart/edev_ui_first_access_step2.png)

![first setup steps 3](./documentation/hugo/static/images/onedev/quickstart/edev_ui_first_access_step3.png)

![first setup steps 4](./documentation/hugo/static/images/onedev/quickstart/edev_ui_first_access_step4.png)

* Add your SSH Key to your your OneDev User :


![add ssh key](documentation/hugo/static/images/onedev/quickstart/onedev_add_ssh_key.png)

* test your SSH Key :


```bash
export ONEDEV_SSH_PORT="6611"
export ONEDEV_IP_ADDR="192.168.1.103"
export MY_SSH_KEY_PATH='~/.ssh.perso.backed/id_rsa'
ssh -Tvai ${MY_SSH_KEY_PATH} git@${ONEDEV_IP_ADDR} -p ${ONEDEV_SSH_PORT}

```

* create a new onedev "project" named `pokus-test-react-app` : it will create a new git repository i guess

![create a new onedev "project"](./documentation/hugo/static/images/onedev/quickstart/onedev-quickstart-create-first-repo.png)

* then pokus-test-react-app


```bash
export ONEDEV_PRJ_NAME="pokus-test-react-app"
export ONEDEV_IP_ADDR="192.168.1.103"
export ONEDEV_HTTP_PORT="6610"
export ONEDEV_SSH_PORT="6611"
export GIT_SSH_COMMAND='ssh -i ~/.ssh.perso.backed/id_rsa -p 6611'

npm i -g create-react-app
npx create-react-app "${ONEDEV_PRJ_NAME}"
cd ${ONEDEV_PRJ_NAME}/
git init
git remote remove onedev
git remote remove onedev_http

git remote add onedev_http http://${ONEDEV_IP_ADDR}:${ONEDEV_HTTP_PORT}/${ONEDEV_PRJ_NAME}
# one dev is a bit different than github/gitlab, its ssh://... instead of git@...
git remote add onedev ssh://${ONEDEV_IP_ADDR}:${ONEDEV_SSH_PORT}/${ONEDEV_PRJ_NAME}

git add -A && git commit -m "init src code"

git push -u onedev master:master

```

## What I would dream of in one development

* there is no concept of labels only of type and priorty on issues, i would want labelling feature :

![onedev no label ](./documentation/hugo/static/images/onedev/quickstart/onedev_issues_do_not_have_labels.png)

* I want to be able to customize KAnban dashboard, I am not happy with the column number and columns names :

![onedev no label](./documentation/hugo/static/images/onedev/quickstart/onedev_kanban_board.png)


## Further Assessment

What will be very important in assessing OneDev : How open is it to the world, or how far does it go into integration with other openb source projects ? IS is goin g to be another gitlab big boat that wants to be your whole world ?


## Kubernetes setup

### `k3d`

> https://medium.com/nerd-for-tech/onedev-with-kubernetes-and-letsencrypt-c63d16a3a31
