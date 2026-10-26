# Padrões de Qualidade e Código Limpo para Novas Implementações e Melhorias
Esta regra deve ser seguida sempre que criar novo código, implementar melhorias, novas telas, componentes, endpoints ou regras de negócio (C#, TypeScript, etc.).
---
## 1. Métricas de Tamanho e Complexidade
- **Tamanho:** Mire em funções que caibam numa tela (~20 linhas) e com poucos níveis de aninhamento (idealmente até 2). Não force: quebrar demais em funções de uma linha sem significado piora a leitura.
- **Função principal apenas orquestra:** A função chamadora deve ler como um resumo do algoritmo (filtrar, ordenar, delegar, finalizar), deixando detalhes específicos para métodos auxiliares.
- **Redução de aninhamento:** Prefira retornos antecipados (*early returns / guard clauses*) no início do método em vez de acumular blocos `if/else` profundamente aninhados.
---
## 2. Nomenclatura e Coesão
- **Responsabilidade Única (SRP):** Cada função deve resolver apenas um objetivo claro. Se o nome necessita de conectivos como "E" (ex.: `ValidarESalvar`), separe em métodos distintos.
- **Nomes autoexplicativos:** Utilize nomes que dispensem comentários para explicar o *que* o código faz.
  - Verbo + Objeto no padrão da linguagem (PascalCase em C#, camelCase em TypeScript).
  - Prefixos semânticos: `Obter...` (busca/leitura), `Criar...`/`Mapear...` (construção/transformação), `Eh...`/`Possui...` (booleano), `Validar...` (validação de regras).
- **Sem abreviações crípticas:** Não utilize variáveis de uma única letra ou termos genéricos como `data`, `item`, `obj`, `aux`, `temp`. Descreva a entidade explicitamente (ex.: `periodoVigente`, `dadosConvenio`).
- **Idioma do projeto:** Mantenha estritamente o idioma predominante no arquivo ou módulo em que estiver atuando (se o módulo estiver em português, continue em português; não misture idiomas).
---
## 3. Qualidade e Boas Práticas
- **Sem duplicação:** Não duplique blocos de validação, formatação ou transformação de dados. Crie funções utilitárias ou métodos privados reutilizáveis.
- **Efeitos colaterais controlados:** Prefira funções puras (que recebem parâmetros e retornam o resultado) a funções que alteram estados globais ou propriedades de classes de forma implícita.
- **Tratamento de nulos e bordas:** Sempre trate valores nulos, vazios ou indefinidos antecipadamente, garantindo retornos padrão consistentes (`"-"`, arrays vazios, etc.).
---
## 4. Verificação Pós-Implementação
- Toda implementação deve ser validada após a edição rodando o build ou testes da solução (`npm run build`, `dotnet build`, `dotnet test`), corrigindo qualquer inconsistência antes de concluir.
