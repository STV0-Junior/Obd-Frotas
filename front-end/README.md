# Front-end

Esta pasta reúne a interface visual do OBD Monitor. A ideia é manter aqui os arquivos da página e do dashboard, organizados por responsabilidade para facilitar manutenção e evolução.

## Organização

- `index.html`: estrutura e conteúdo das páginas.
- `css/`: estilos, layout, cores, tipografia e ajustes responsivos.
- `js/`: interações da interface e apresentação dos dados recebidos.
- `assets/` ou `images/`: ícones, imagens e outros recursos visuais.

No estado atual, `index.html` é uma página de apresentação independente. Seus estilos e a pequena interação do menu ainda estão no próprio arquivo. Conforme a interface crescer, eles podem ser separados nos diretórios acima.

## Diretrizes

- Mantenha a apresentação visual separada da comunicação com o adaptador e das regras de cálculo.
- Identifique claramente dados de demonstração; não os apresente como leituras reais do veículo.
- Prefira componentes e estilos reutilizáveis e mantenha o layout adaptável a telas pequenas.
- Não armazene senhas, tokens ou outros segredos nos arquivos do front-end.

O dashboard pode exibir apenas informações que uma fonte de dados realmente forneça. A integração entre a interface e o conector OBD-II ainda precisa ser desenvolvida.