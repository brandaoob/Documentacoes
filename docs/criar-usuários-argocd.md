Documentação para te ajudar a criar usuarios no ArgoCd

Como criar o usuário no ArgoCd

Portanto, quando instalamos o argocd no cluster kubernetes, ele cria os yamls no namespace argocd. Que são os serviços, implantações, rbac etc. 

Edite o ConfigMap argocd-cm adicionando o nome dos usuários e o método que ele irá acessar via web ( nesse caso será via login ), rodaremos o comando: `k edit configmaps argocd-cm` 
para adicionarmos o nome do usuário e o método de acesso.

Como podemos ver um exemplo na imagem abaixo:

![image](https://user-images.githubusercontent.com/93404162/222238011-68645ba2-1cfe-4052-9832-09ffdafd2446.png)


Edite o ConfigMap argocd-rbac-cm adicionando as permissões que o usuário terá dentro do argocd, rodaremos o comando: 
`k edit configmaps argocd-rbac-cm`
para adicionarmos as permissões que o usuário terá.

Como podemos ver um exemplo de permissões na imagem abaixo:

![image](https://user-images.githubusercontent.com/93404162/222238098-6df382ec-b3f0-46d8-aee2-0a16cb458f59.png)


Após os passos acima forem concluidos, no namespace argocd iremos entrar dentro do pod argocd-server, para entrarmos dentro do pod rodaremos o comando : `k exec -it argocd-server-5f7bbd5bdf-vzvxg -- bash`

Como descreve a imagem abaixo:

![image](https://user-images.githubusercontent.com/93404162/222238219-d1af8360-5979-4648-8dd0-e09ca6d80334.png)

Logo após entrarmos no pod, iremos fazer o login no ArgoCd dentro do pod/argocd-server para podermos fazer o update da senha do nosso usuário.
Para fazermos o login no ArgoCd pelo pod/argocd-server iremos precisar do IP do server do pod/argocd-server, para pegar esse IP rodaremos o comando: 
`k get all -n argocd`

Após rodar esse comando irá aparecer todos os serviços que estão no namespace argocd, lá poderemos ver o IP do pod/argocd-server

Como mostra a imagem abaixo:

![image](https://user-images.githubusercontent.com/93404162/222238320-4622c008-4237-4b33-adeb-cb8e66ac7e3f.png)

Com o IP do pod/argocd-server em mãos iremos fazer login no ArgoCd via pod, para isso iremos rodar o comando: 
`argocd login 172.20.174.101`

**Obs** ele irá pedir a senha de admin para poder autenticar, tenha essa senha em mãos.

Como descreve a imagem abaixo:

![image](https://user-images.githubusercontent.com/93404162/222238598-a6a35138-8ad3-4b6e-84cc-6a11cf8068da.png)

Após login feito iremos fazer o update da senha do usuários que criamos na etapa anterior, para isso rodaremos o comando: 
`argocd account update-password --account usuário-criado --new-password password`

**Obs** ele também irá pedir a senha do usuário admin para prosseguir com a ação requerida, por tanto, tenha essa senha em mãos.

após adicionarmos a senha do user admin, irá aparcer a seguinte mensagem: Password updated
que significa que o update da senha foi concluido com sucesso!

Como nos mostra a imagem abaixo:

![image](https://user-images.githubusercontent.com/93404162/222239027-611f3262-6863-4b69-b447-72dd67b9761f.png)

Com o update concluido iremos testar o acesso criado via WEB

Como descreve as imagens abaixo:

![Captura de tela de 2023-03-01 16-07-27](https://user-images.githubusercontent.com/93404162/222240620-49a74955-79c5-4be0-a541-f2844c89ce3b.png)
![image](https://user-images.githubusercontent.com/93404162/222240648-67a1697c-1e5a-4bd6-8b23-ee5eb67d06c2.png)

Agora com tudo testado, agora só aproveitar as vantagens do ArgoCd :)
