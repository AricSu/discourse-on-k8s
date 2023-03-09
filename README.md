# discourse-on-k8s

It's a tool to build discourse on k8s(adapted to apple silicon system or arm chip)

## Why I do this

First, I'm a rookie who's learning [k8s](https://kubernetes.io/) and [discourse](https://github.com/discourse/discourse) without familiar with ruby. Because both are very popular on current tech-world, and some good products are using them, like [tidb-operator](https://github.com/pingcap/tidb-operator) or [AskTUG](https://tidb.net/u/jansu-dev/post/all).  
**Second, I‘ve build [my blog website](http://www.dbnest.net/) focusing on which tech learning, and wanna find out a way to communicate with others people.**
Third, my website was running on my macbook-pro-m1, It's also a big challange to make discourse run on Apple Silicon system.

So, I made this tool or repo based on reasons above, furthermore, I know how difficult and wasting-time it does, I wanna simplify it for everyone.

## Quickstart

## Details-demo

1. You should install k8s and docker-desktop, firstly, on your mac, and some steps from ChatGPT may help you. More details on [the docker website](https://www.docker.com/products/docker-desktop/).

2. Before finish this project, you may wanna build or learn how it implmented. You can do thing below to look more details:

    ```shell
    git clone https://github.com/jansu-dev/discourse-on-k8s.git
    cd discourse-on-k8s/demo

    kubectl apply -f volumns.yaml
    kubectl apply -f redis.yaml

    # please replace XXX into you own values
    kubectl create secret generic secret --from-literal=dbUsername=XXX --from-literal=dbPassword='XXX' --from-literal=smtpUsername=XXX --from-literal=smtpPassword=XXX --dry-run=client -o yaml > discourse-secret.yaml

    kubectl apply -f postgres.yaml
    kubectl apply -f discourse.yaml
    kubectl apply -f ingress.yaml


    kubectl port-forward psql 5433:5432
    pg_restore -U discourse -d discourse -p 5433 -h localhost discourse.dump -W
    ```

## Thanks

1. Thanks for [discourse community](https://meta.discourse.org/tag/arm) and [discourse blog](https://blog.discourse.org/2021/12/2021-12-07-discourse-on-a-raspberry-pi/), I got the feeling running discourse-on-m1 is possible, and though, a rookie can learn discourse with abundant experiences as fast and easy as eating food.
2. Thanks for [oursky/discourse-k8s](https://github.com/oursky/discourse-k8s), this repo let me know how to implement moving docker into k8s step by step, really appreciate this sharing.
3. Thanks really for others who already gave many suggestions and experiences, I couldn't finish it without your help.
4. Thanks for [ChatGPT](https://chat.openai.com/chat), without you, I couldn't know every implment details to a rookie.
