# Status do Projeto - Atualizado em 2026-05-22

## Autentificação & Usuários ✅
- [] Registro de novos usuários
- [] Login com emissão de token JWT
- [ ] Proteção de rotas por papel (admin/customer)
- [ ] Seed de usuários (admin e customer)

## Catálogo de Produtos 🟡
- [] CRUD completo de produtos
- [ ] Filtros por categoria, faixa de preço e nome
- [ ] Paginação
- [ ] Upload/validação de imagem do produto
- [ ] Soft delete (diferencial)

## Carrinho de Compras ❌
- [ ] Carrinho persistente por usuário
- [ ] Adicionar item com validação de estoque
- [ ] Remover item
- [ ] Atualizar quantidade
- [ ] Limpar carrinho
- [ ] Garantir um único carrinho por usuário autenticado

## Checkout & Pedidos ❌
- [ ] Reserva atômica de estoque (contra overselling)
- [ ] Cálculo do total com preços vigentes no momento
- [ ] Máquina de estados: PENDING → PAID → SHIPPED → DELIVERED
- [ ] Cancelamento antes de SHIPPED com devolução de estoque
- [ ] Simulação de pagamento (sucesso/falha)
- [ ] Pagamento real com gateway + webhook (diferencial)
- [ ] Idempotência no checkout (diferencial)

## Cupons de Desconto ❌
- [ ] Cupons percentuais e de valor fixo
- [ ] Validação de data de expiração
- [ ] Uso único por usuário
- [ ] Valor mínimo do pedido
- [ ] Aplicação no checkout antes do cálculo final

## Regras Transversais Obrigatórias ❌
- [ ] Todos os 5 domínios implementados e funcionais
- [ ] Validação de entrada nas bordas (Bean Validation)
- [ ] Respostas de erro padronizadas (sem stack traces)
- [ ] Migrations (Flyway) para schema reproduzível
- [ ] Script de seed para dados de exemplo
- [ ] Testes automatizados (cobertura crítica)
- [ ] Rate limiting em endpoints públicos
- [ ] Cache de produtos com Redis (invalidação)
- [ ] Logs JSON por requisição (timestamp, rota, status, duração)
- [ ] Documentação OpenAPI/Swagger interativa

## Infraestrutura & CI/CD ❌
- [ ] Pipeline CI (GitHub Actions) com build e testes
- [ ] Rate limiting implementado
- [ ] Redis em desenvolvimento/produção
- [ ] Health check e métricas (diferencial)
- [ ] Deploy automatizado (diferencial)

## Interface Web ❌
- [ ] Consumo da API (React ou outra)
- [ ] Páginas: login, registro, listagem de produtos
- [ ] Carrinho e checkout
- [ ] Painel admin para produtos e pedidos
- [ ] Aplicação de cupons