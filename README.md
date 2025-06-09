Como executar o projeto
1 - Clone o projeto 
2 - Execute no terminal:

<img width="1154" alt="Captura de Tela 2025-06-08 às 14 47 57" src="https://github.com/user-attachments/assets/413eab1f-7a90-44b9-9597-89b20112b6d3" />

Funcionalidades
Desenvolvi um sistema para uma locadora de filmes que utiliza uma pilha para armazenar os filmes escolhidos pelo usuário, seguindo a lógica LIFO (último a entrar, primeiro a sair). Além disso, implementei a funcionalidade de salvar o histórico dessas escolhas em um arquivo .txt. Assim, mesmo que o programa seja fechado, o usuário pode consultar o histórico dos últimos filmes alugados ao reabrir o sistema.
Os filmes ficaram dessa forma:

<img width="1153" alt="Captura de Tela 2025-06-08 às 15 10 26" src="https://github.com/user-attachments/assets/c86519ac-1302-4071-a7a4-4d7675c2486d" />

Desfazendo último aluguel
Como vocês podem ver por essa imagem, o último filme alugado pode ser desfeito facilmente. Essa funcionalidade é possível graças ao uso da estrutura de pilha, que permite remover rapidamente o item que está no topo ou seja, o filme mais recentemente alugado. Dessa forma, caso o usuário mude de ideia ou tenha cometido um erro, ele pode corrigir a ação com apenas um comando, mantendo o controle total sobre sua lista de aluguéis.

<img width="1129" alt="Captura de Tela 2025-06-08 às 15 18 24" src="https://github.com/user-attachments/assets/8c839342-d3ed-4cef-9da7-432f0cb8b1d6" />

Mostrando o histórico de aluguéis

Nesta parte do sistema, é possível visualizar todo o histórico de filmes alugados, exibindo-os do mais recente para o mais antigo. Isso é feito percorrendo a pilha de cima para baixo, mantendo a ordem em que os filmes foram adicionados. Além disso, com a integração do arquivo .txt, esse histórico é salvo automaticamente, permitindo que os dados sejam recuperados mesmo após o fechamento do programa. Além disso, como eu já deixei alguns filmes previamente registrados, é possível observar que o histórico aparece automaticamente ao iniciar o programa. Isso comprova que o arquivo .txt está funcionando corretamente, armazenando os dados mesmo após o encerramento do sistema e permitindo que o histórico seja carregado na próxima execução.

<img width="1150" alt="Captura de Tela 2025-06-08 às 15 28 15" src="https://github.com/user-attachments/assets/8ff9118d-e698-4792-9917-8cd2518da043" />



