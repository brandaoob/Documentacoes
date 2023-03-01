Documentação para te ajudar a criar usuarios no ArgoCd

Como criar o usuário no ArgoCd

Portanto, quando instalamos o argocd no cluster kubernetes, ele cria os yamls no namespace argocd. Que são os serviços, implantações, rbac etc. 

Edite o ConfigMap argocd-cm adicionando o nome dos usuários e o método que ele irá acessar via web ( nesse caso será via login ), podemos ver um exemplo na imagem abaixo:





Edite o ConfigMap argocd-rbac-cm adicionando as permissões que o usuário terá dentro do argocd, podemos ver um exemplo de permissões na imagem abaixo:







Após os passos acima forem concluidos, no namespace argocd iremos entrar dentro do pod argocd-server, para entrarmos dentro do pod rodaremos o comando : k exec -it argocd-server-5f7bbd5bdf-vzvxg -- bash
Como descreve a imagem abaixo:




Logo após entrarmos no pod, iremos fazer o login no ArgoCd dentro do pod/argocd-server para podermos fazer o update da senha do nosso usuário.
Para fazermos o login no ArgoCd pelo pod/argocd-server iremos precisar do IP do server do pod/argocd-server, para pegar esse IP rodaremos o comando : k get all -n argocd
Após rodar esse comando irá aparecer todos os serviços que estão no namespace argocd, lá poderemos ver o IP do pod/argocd-server
Como mostra a imagem abaixo:



Com o IP do pod/argocd-server em mãos iremos fazer login no ArgoCd via pod, para isso iremos rodar o comando : argocd login 172.20.174.101 
OBS : ele irá pedir a senha de admin para poder autenticar, tenha essa senha em mãos.
Como descreve a imagem abaixo:


Após login feito iremos fazer o update da senha do usuários que criamos na etapa anterior, para isso rodaremos o comando : argocd account update-password --account usuário-criado --new-password passwword
OBS : ele também irá pedir a senha do usuário admin para prosseguir com a ação requerida, por tanto, tenha essa senha em mãos.
após adicionarmos a senha do user admin, irá aparcer a seguinte mensagem: Password updated
que significa que o update da senha foi concluido com sucesso!
Como nos mostra a imagem abaixo:





Com o update concluido iremos testar o acesso criado via WEB
Como descreve a imagem abaixo: