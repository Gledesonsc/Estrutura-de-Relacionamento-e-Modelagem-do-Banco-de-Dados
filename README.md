### Estrutura de Relacionamento e Modelagem do Banco de Dados
---
## 📁 Estrutura do Banco de Dados

### 🗄️ Entidades Principais:

1. **User** (Tabela: `users`)
   - `id`: UUID (Primary Key)
   - `username`: String (Unique)
   - `email`: String (Unique)
   - `password`: String (Hashed)
   - `profile_photo`: String (URL para a foto de perfil)
   - `role`: Enum (`Admin`, `Director`, `Reporter`, `Editor`)
   - `created_at`: DateTime
   - `updated_at`: DateTime

2. **Card** (Tabela: `cards`)
   - `id`: UUID (Primary Key)
   - `code`: String (Unique)
   - `type`: Enum (`IPH01` a `IPH05`, `CT01` a `CT27`)
   - `status`: Enum (`In`, `Out`, `Under Review`)
   - `location`: String (Ilha de edição ou UPJ)
   - `created_at`: DateTime
   - `updated_at`: DateTime

3. **Program** (Tabela: `programs`)
   - `id`: UUID (Primary Key)
   - `name`: Enum (`ARENA`, `CHEGA MAIS`, `PATRULHA DA CIDADE`, `JORNAL DO DIA`, `TÁ NA HORA RN`, `Outro`)
   - `created_at`: DateTime
   - `updated_at`: DateTime

4. **Cameraman** (Tabela: `cameramen`)
   - `id`: UUID (Primary Key)
   - `name`: String (Unique)
   - `created_at`: DateTime
   - `updated_at`: DateTime

5. **Reporter** (Tabela: `reporters`)
   - `id`: UUID (Primary Key)
   - `name`: String (Unique)
   - `created_at`: DateTime
   - `updated_at`: DateTime

6. **Service** (Tabela: `services`)
   - `id`: UUID (Primary Key)
   - `user_id`: UUID (Foreign Key para `users`)
   - `card_id`: UUID (Foreign Key para `cards`)
   - `program_id`: UUID (Foreign Key para `programs`)
   - `cameraman_id`: UUID (Foreign Key para `cameramen`)
   - `reporter_id`: UUID (Foreign Key para `reporters`)
   - `retransmission_note`: Text
   - `sequence`: Text
   - `observation`: Text
   - `file_upload`: String (URL para arquivos)
   - `created_at`: DateTime
   - `updated_at`: DateTime

7. **AuditLog** (Tabela: `audit_logs`)
   - `id`: UUID (Primary Key)
   - `user_id`: UUID (Foreign Key para `users`)
   - `action`: Enum (`Create`, `Update`, `Delete`)
   - `entity`: String (Entidade modificada)
   - `entity_id`: UUID (ID da entidade modificada)
   - `changes`: JSON (Descrição das alterações)
   - `timestamp`: DateTime

### 🔗 Relacionamentos:
- **User** tem muitos **Service**.
- **Card** pode ser usado em muitos **Service**.
- **Program** pode estar relacionado a muitos **Service**.
- **Cameraman** pode participar de muitos **Service**.
- **Reporter** pode participar de muitos **Service**.
- **Service** é auditado por **AuditLog**.

## 🎨 Diagrama UML

Um diagrama UML foi gerado para representar essas entidades e seus relacionamentos, ajudando na visualização da estrutura do sistema.

![Diagrama UML](#)

## 📝 Passo a Passo para Implementação

### 1. **Setup do Projeto**
   - **Frontend:** Inicializar um projeto React utilizando `create-react-app` ou similar.
   - **Backend:** Inicializar um projeto Node.js com Sequelize configurado para PostgreSQL.

### 2. **Configuração do Banco de Dados**
   - Criar o banco de dados no PostgreSQL.
   - Criar as tabelas conforme as entidades descritas acima.

### 3. **Desenvolvimento do Backend**
   - Configurar os modelos Sequelize para cada entidade.
   - Implementar as rotas para CRUD de cada entidade.
   - Implementar o sistema de login com reCAPTCHA e middleware de autenticação.
   - Implementar a lógica de auditoria utilizando `AuditLog`.

### 4. **Desenvolvimento do Frontend**
   - Configurar o React Hook Form para criar e validar os formulários.
   - Implementar os componentes de interface para o painel administrativo e formulários.
   - Implementar a lógica de bloqueio de campos para evitar edição concorrente.

### 5. **Teste e Depuração**
   - Testar as funcionalidades em ambientes de desenvolvimento e produção.
   - Realizar depuração e otimização conforme necessário.

---
