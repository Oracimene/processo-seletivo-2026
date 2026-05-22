# Regras de Negócio – E-commerce Simplificado

## 1. Autenticação & Usuários

| ID | Regra de Negócio |
|----|------------------|
| **AUTH-01** | O sistema deve permitir registro de novos usuários com credenciais válidas. |
| **AUTH-02** | O sistema deve permitir login e emissão de token de acesso. |
| **AUTH-03** | Dois papéis de usuário devem existir: `admin` (gerencia produtos e pedidos) e `customer` (realiza compras). |
| **AUTH-04** | Rotas da API devem ser protegidas e acessíveis apenas conforme o papel do usuário (RBAC). |

## 2. Catálogo de Produtos

| ID | Regra de Negócio |
|----|------------------|
| **PROD-01** | O sistema deve permitir CRUD completo de produtos (criar, listar, detalhar, atualizar, remover). |
| **PROD-02** | Cada produto deve possuir os campos: nome, descrição, preço, estoque, categoria, imagem. |
| **PROD-03** | A listagem de produtos deve suportar filtros por categoria, faixa de preço e nome (busca textual). |
| **PROD-04** | A listagem de produtos deve ser paginada. |

## 3. Carrinho de Compras

| ID | Regra de Negócio |
|----|------------------|
| **CART-01** | O carrinho deve ser persistido (não efêmero), mantendo os itens entre sessões. |
| **CART-02** | Cada usuário autenticado pode ter apenas um carrinho ativo. |
| **CART-03** | Operações permitidas no carrinho: adicionar item, remover item, atualizar quantidade, limpar carrinho. |
| **CART-04** | Ao adicionar item, deve ser validado se a quantidade solicitada está disponível em estoque. |
| **CART-05** | A mesma validação de estoque deve ser repetida no momento do checkout. |

## 4. Checkout & Pedidos

| ID | Regra de Negócio |
|----|------------------|
| **CHECK-01** | A reserva de estoque durante o checkout deve ser atômica: duas requisições simultâneas para o último item disponível não podem ambas ter sucesso. |
| **CHECK-02** | O valor total do pedido deve ser calculado com base nos preços vigentes no momento do checkout (não no momento da adição ao carrinho). |
| **CHECK-03** | O pedido deve seguir a máquina de estados: `PENDING → PAID → SHIPPED → DELIVERED`. |
| **CHECK-04** | Cancelamento do pedido é permitido apenas antes do estado `SHIPPED`. |
| **CHECK-05** | Ao cancelar um pedido dentro do permitido, o estoque dos produtos deve ser devolvido. |
| **CHECK-06** | O pagamento pode ser simulado (sucesso/falha) ou, opcionalmente, integrado com gateway real (ex: Abacate Pay, Stripe) com webhook. |

## 5. Cupons de Desconto

| ID | Regra de Negócio |
|----|------------------|
| **COUP-01** | Cupons podem ser de dois tipos: percentual de desconto ou valor fixo. |
| **COUP-02** | Cada cupom possui data de expiração; cupons expirados não podem ser aplicados. |
| **COUP-03** | Um cupom pode ter restrição de uso único por usuário (não pode ser reutilizado pelo mesmo usuário). |
| **COUP-04** | O cupom pode exigir um valor mínimo do pedido para ser aplicado. |
| **COUP-05** | A validação do cupom deve ocorrer no checkout, antes do cálculo final do pedido. |

## 6. Regras Transversais Obrigatórias

| ID | Regra de Negócio |
|----|------------------|
| **CROSS-01** | Todos os 5 domínios (autenticação, catálogo, carrinho, checkout, cupons) devem estar implementados e funcionais. |
| **CROSS-02** | Todas as entradas da API devem ser validadas nas bordas (tipos, formatos, campos obrigatórios). |
| **CROSS-03** | As respostas de erro devem ser padronizadas com códigos HTTP apropriados; stack traces não podem ser expostos ao cliente. |
| **CROSS-04** | O banco de dados deve utilizar migrations (ou equivalente) para ser reproduzível do zero. |
| **CROSS-05** | Deve haver um script ou comando para popular o banco com dados de exemplo (seed). |
| **CROSS-06** | Testes automatizados devem cobrir fluxos críticos: checkout, concorrência de estoque e cupons. |
| **CROSS-07** | Endpoints públicos (login, registro, catálogo) devem ter rate limiting. |
| **CROSS-08** | Produtos devem ser cacheados com solução externa (Redis, Memcached, etc.); cache deve ser invalidado ao criar, editar ou remover produto. |
| **CROSS-09** | Toda requisição deve ser logada em formato JSON com timestamp, método, rota, status code e duração. |
| **CROSS-10** | A API deve ter documentação interativa (Swagger/OpenAPI) com exemplos para todos os endpoints. |

## 7. Diferenciais (Pontuação Extra)

| ID | Regra de Negócio (opcional) |
|----|-----------------------------|
| **EXTRA-01** | Produtos removidos devem ter soft delete para preservar integridade de pedidos históricos. |
| **EXTRA-02** | Integração com gateway de pagamento real (Abacate Pay, Stripe) com recebimento de status via webhook. |
| **EXTRA-03** | Observabilidade: métricas, tracing, health check. |
| **EXTRA-04** | Idempotência no checkout (permitir retry seguro). |