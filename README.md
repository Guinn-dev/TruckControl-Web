# TruckControl Web 🚛

Versão web completa do aplicativo TruckControl.  
Adaptado em **HTML + CSS + JavaScript puro**, com integração Firebase nativa.

## Stack

| Camada | Mobile (original) | Web (novo) |
|--------|-------------------|------------|
| Framework | Flutter/Dart | HTML5 + Vanilla JS (ES Modules) |
| Auth | firebase_auth | Firebase Auth SDK v10 |
| Database | cloud_firestore | Firestore SDK v10 |
| UI | Material Widgets | CSS personalizado (design system próprio) |
| Charts | fl_chart | Canvas 2D API nativa |
| Deploy | Google Play / App Store | Qualquer hosting estático |

## Funcionalidades Migradas

### ✅ Autenticação
- Login com e-mail + senha
- Login com Google (popup)
- Persistência de sessão
- Logout seguro

### ✅ Dashboard (Home)
- KPIs em tempo real: caminhões, carretas, manutenções, usuários
- Gráfico de linha: entregas dos últimos 30 dias
- Gráfico de donut: manutenções por status
- Feed de atualizações recentes

### ✅ Frota (Data)
- Listagem de caminhões com busca em tempo real
- Listagem de carretas com busca em tempo real
- Navegação para detalhe do veículo (caminhões)
- Botão de edição para administradores

### ✅ Detalhe do Veículo (VehicleDetail)
- Dados técnicos completos (placa, marca, modelo, chassi, RENAVAM)
- Dados de operação (filial, tecnologia, tipo de operação)
- Composição atual (Carreta 1 / Carreta 2)

### ✅ Manutenção
- Contadores de status (Agendadas / Atrasadas / Concluídas)
- Lista ordenada por data (mais recente no topo)
- Badges coloridos por status

### ✅ Perfil
- Dados do usuário carregados do Firestore
- Avatar com inicial do nome
- Exibe: nome, e-mail, cargo, telefone, filial, tipo

### ✅ Admin Panel
- Aba Caminhões: tabela completa com edição e exclusão
- Aba Carretas: tabela completa com edição e exclusão  
- Aba Usuários: gerenciamento de contas
- Aba Sistema: informações do sistema (zona de perigo protegida)

### ✅ Modais de Cadastro / Edição
- Registrar Caminhão (RegisterFrotaPage)
- Registrar Carreta (RegisterCarretaPage)
- Registrar Usuário (RegisterUserPage)
- Modo edição (carrega dados existentes)
- Campos de auditoria automáticos (last_updated_at, last_updated_by_name)

## Como Usar

### 1. Hospedagem Estática

Basta fazer upload dos dois arquivos em qualquer serviço:
- `index.html`
- `style.css`

Compatível com: Firebase Hosting, Netlify, Vercel, GitHub Pages, etc.

### 2. Firebase Hosting (recomendado)

```bash
firebase init hosting
# Selecione o projeto frota-39c83
# Public directory: . (raiz ou pasta com os arquivos)
firebase deploy
```

### 3. Desenvolvimento Local

Devido à política CORS do Firebase, use um servidor local:

```bash
# Python
python3 -m http.server 8080

# Node.js
npx serve .

# VS Code: extensão Live Server
```

Acesse: `http://localhost:8080`

## Estrutura de Coleções Firestore

```
caminhoes/         → placa, marca, modelo, ano_modelo, cor, chassi, renavam,
                     filial, tecnologia, operacao, status
carretas/          → placa, modelo, marca, cor, ano_fabricacao, ano_modelo,
                     renavam, chassi, capacidade, cavalo_atual
composicoes/       → id_cavalo, id_carreta1, id_carreta2, last_updated_*
manutencoes/       → placa_veiculo, tipo_servico, status, data, custo
entregas/          → id_caminhao, volume_m3, data, status
usuarios/          → nome, email, tipo (admin|motorista), cargo, telefone, filial
```

## Credenciais de Teste

As credenciais de acesso estão no Firebase Authentication do projeto `frota-39c83`.  
Solicite ao administrador do projeto.

## Diferenças em relação ao app mobile

| Feature | Mobile | Web |
|---------|--------|-----|
| Criação de usuário sem deslogar admin | Instância Firebase secundária | ⚠️ Requer Cloud Function para implementação completa |
| Charts interativos | fl_chart | Canvas API (funcional) |
| Navegação | Navigator/Routes | Hash-based SPA sem library |
| Offline | Flutter cache | Firestore cache automático |
| Push notifications | Firebase Messaging | Não implementado |
