# Principais comandos do Git

- Iniciando um Repositório

  ```git init```

- Listando Arquivos Modificados

  ```git status```

- Desfazendo Alterações

	- Arquivos não monitorados

		```git checkout```
	
	- Para apagar novos arquivos que ainda não foram adicionados ao Stage

		```git clean -df```
	
	- Removendo arquivos do Stage

		```git reset```
	
	-  Desfazendo o último commit

		```git revert HEAD```

- Renomear Commit

	```git commit —amend```

- Branches
	- Listando Branches locais

	  ```git branch```
	
	- Listar também as branches que estão no repositório remoto

	  ```git branch -a```
	
	- Indo para outra branch

	  ```git checkout minha-branch```
	
	- Se você adicionar -b uma nova branch será criada
  
	  ```git checkout -b minha-nova-branch```
	
	- Excluindo branches

      ```git branch -d nome-da-branch // normal```
      
      ```git branch -D nome-da-branch // forçando```
	
	- Renomeando branches

	  ```git branch -m novo-nome-da-branch```
	
	- Se você estiver em uma branch e quiser renomear outra, você deve passar primeiro o nome atual da branch que quer renomear:

	  ```git branch -m nome-atual novo-nome```

	- Branch Órfã
		Uma branch órfã tem esse nome porque ela não está ligada à branch principal, então 
		seus históricos não são compartilhados.
	
  ```shell
    Exemplo: 
      i---j---k     <== branch 'minha branch'
            /
    a---b---c---d---h---l   <== branch 'main'
        \         /
          e---f---g         <== branch 'minha outra branch'
    
    1---2---3---4           <== branch `órfã`
  ```

  Isso pode ser útil quando você quer colocar mais de um projeto em um mesmo 
  repositório. Um bom exemplo é quando você tem um projeto no Github e quer criar 
  um site para divulgar o seu projeto. A aplicação e o site são coisas diferentes,
  portanto os códigos deles devem ser versionados separadamente.
  Ter ambos em um mesmo repositório simplifica o gerenciamento.

  Para criar uma branch órfã basta usar o comando:

    ```git checkout --orphan minha-branch-orfa```

- Visualizando o Histórico de Commits

  ```git log```

	- Histórico de um ou mais arquivos

	  ```git log -p meus-arquivos```

	- Histórico de um autor

	  ```git log --autor=name-author```

	- Histórico por data

	  ```git log --after="MMM DD YYYY"```

	  ```git log --before="MMM DD YYYY"```

	- Histórico Baseado em uma mensagem(commit)

	  ```git log --grep produtos```

    Com esse comando teremos o histórico de commits em que a mensagem do commit 
    possua a palavra “produtos”. O que passamos pode ser uma expressão regular, 
    e podemos passar mais de uma:
	
	Exemplos:

	Procurar por "produtos" OU "usuarios"

  ```git log --grep produtos --grep usuarios```
	
	Procurar por "produtos" E "usuarios"

  ```git log --grep produtos --and --grep usuarios```

- Exibir branches em um modo mais legível

  É possível mandar imprimir o histórico exibindo as branches do repositório com algo 
  mais legível e com cores com um comando. Teremos um resultado parecido com esse:

  ```shell
    * a102055 (HEAD -> master) commit 8
    | * 196d28e (branch-2) commit 7
    | * 07e073c commit 3
    | * 2b077ca new fie
    | | * c1369d8 (branch-3) commit 6
    | | * d11bdcd commit 5
    | |/
    |/|
    * | 2b22b75 commit 2
    |/
    * d5a12b0 .gitignore
    * 9535426 -- commit 1
  ```

  O comando é um pouco comprido:

  ```git log --all --decorate --oneline --graph```

  Para decorar tudo o que devemos escrever depois do log.
  ```
    --all
    --decorate
    --oneline
    --graph
  ```

- Trabalhando em mais de uma coisa sem fazer commit

  Pode haver momentos em que você precisa parar o que está fazendo e começar a trabalhar 
  em outra tarefa. Porém, pode não é bom fazer o commit de algo que ainda não foi 
  finalizado para depois voltar nele, resultando em um commit que ficará no histórico 
  mas que possui um código que não funciona. Nós podemos salvar essas alterações feitas 
  mesmo sem precisar realizar um commit para depois voltar a trabalhar nela, o que é 
  chamado de Stash (algo como “esconder” ou “acumular”).

  Ao fazer isso, seu repositório voltará ao estado do último commit, e as alterações 
  feitas anteriormente estarão “escondidas”.

    - Salvando modificações em um Stash
    
      ```git stash```

    - Você ainda pode colocar um nome nesse stash
    
      ```git stash push -m meu-nome-stash```

    - Listando Stash
    
      ```git stash list```
    
    - Recuperando modificações
    
      ```git stash apply```

	Isso vai recuperar o código do stash mais recente. Se quiser recuperar um stash 
	mais antigo, basta ver o número do stash que aparece quando o listamos e passar 
	para o seguinte comando:

    ```git stash apply stash@{2}```

	- Removendo Stashes
    
      Quando nós recuperamos alterações de um stash, ele continua guardado. Para apagá-lo 
      da pilha, execute o comando drop junto ao nome do stash que você quer remover
      
      ```git stash drop stash@{5}```

- Juntando alguns pedaços do trabalho
Pode ser que você esteja trabalhando em uma branch e queira fazer o merge do código 
dela com outra branch, mas não quer juntar o trabalho inteiro, apenas um commit 
específico. Isso é possível com o Cherry Pick.

  ```git cherry-pick id-do-commit```
