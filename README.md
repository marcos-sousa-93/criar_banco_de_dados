# criar_banco_de_dados
## Criando banco de dados em C#
# 1 Instalar os Pacotes Necessários:
## No Gerenciador de Pacotes NuGet, adicione os seguintes pacotes ao seu projeto:
<pre>
    <code>
        <h3>Install-Package Microsoft.EntityFrameworkCore</h3>
    </code>
</pre>
<pre>
    <code>
        <h3>Install-Package Microsoft.EntityFrameworkCore.SqlServer</h3>
    </code>
</pre>
<pre>
    <code>
        <h3>Install-Package Microsoft.EntityFrameworkCore.Tools</h3>
    </code>
</pre>

# 2 Criar o Modelo (Classes):
## Crie classes Pessoa que representem as tabelas do banco de dados. Por exemplo:
<pre>
    <code>
        <h3>
public class Pessoa {
    public int Id { get; set; }
    public string Nome { get; set; }
    public string Email { get; set; }
}
        </h3>
    </code>
</pre>

# 3 Criar o Contexto do Banco de Dados:
## Crie uma classe CadastroPessoaContext que herda de DbContext e define as DbSet para as entidades:
<pre>
    <code>
        <h3>
public class CadastroPessoaContext : DbContext {
    public DbSet<Pessoa> Pessoas { get; set; }
    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder) {
        optionsBuilder.UseSqlServer(@"Server=(localdb)\mssqllocaldb;Database=CadastroPessoaDB;Trusted_Connection=True;");
    }
}
        </h3>
    </code>
</pre>

# 4 Criar as Migrations:
## No Gerenciador de Pacotes NuGet, rode o comando para criar a migration inicial:
<pre>
    <code>
        <h3>
Add-Migration InitialCreate
        </h3>
    </code>
</pre>

# 5 Atualizar o Banco de Dados:
## Aplique a migration para criar o banco de dados:
<pre>
    <code>
        <h3>
Update-Database
        </h3>
    </code>
</pre>

# 6 Adicionar Dados ao Banco de Dados
## Agora que tudo está configurado, você pode adicionar dados ao banco de dados.
## Passo 1: Criar uma Instância do Contexto
<pre>
    <code>
        <h3>
class Program {
    static void Main(string[] args) {
        using (var context = new CadastroPessoaContext()) {
            // Agora você pode adicionar dados ao banco de dados usando o contexto
        }
    }
}
        </h3>
    </code>
</pre>

# Passo 2: Criar uma Instância do Objeto a Ser Adicionado
## Dentro do using (var context = new CadastroPessoaContext()) { } colocar:
<pre>
    <code>
        <h3>
var novaPessoa = new Pessoa {
    Nome = "Maria Silva",
    Email = "maria.silva@example.com"
};
        </h3>
    </code>
</pre>

## exemplo:
<pre>
    <code>
        <h3>
class Program {
    static void Main(string[] args) {
        using (var context = new CadastroPessoaContext()) {
            var novaPessoa = new Pessoa {
                Nome = "Maria Silva",
                Email = "maria.silva@example.com"
            };
        }
    }
}
        </h3>
    </code>
</pre>

# Passo 3: Adicionar o Objeto ao Contexto
<pre>
    <code>
        <h3>
context.Pessoas.Add(novaPessoa);
        </h3>
    </code>
</pre>

# Passo 4: Salvar as Mudanças no Banco de Dados
<pre>
    <code>
        <h3>
context.SaveChanges();
        </h3>
    </code>
</pre>

## Aqui está o código:
<pre>
    <code>
        <h3>
class Program {
    static void Main(string[] args) {
        using (var context = new CadastroPessoaContext()) {
            var novaPessoa = new Pessoa {
                Nome = "Maria Silva",
                Email = "maria.silva@example.com"
            };
            context.Pessoas.Add(novaPessoa);
            context.SaveChanges();
            Console.WriteLine("Dados inseridos com sucesso!");
        }
    }
}
        </h3>
    </code>
</pre>

# Recuperar os Dados do Banco de Dados
## Agora, vamos recuperar os dados armazenados no banco de dados e exibi-los no console.
# Passo 1: Criar uma Instância do Contexto
## Primeiro, você precisa criar uma instância do contexto para interagir com o banco de dados:
<pre>
    <code>
        <h3>
using (var context = new CadastroPessoaContext()) {
    // A partir daqui, você pode acessar os dados do banco
}
        </h3>
    </code>
</pre>

# Passo 2: Recuperar os Dados Usando LINQ
## Use o LINQ (Language Integrated Query) para consultar os dados da tabela Pessoas. Por exemplo, para buscar todos os registros:
<pre>
    <code>
        <h3>
var pessoas = context.Pessoas.ToList();
        </h3>
    </code>
</pre>

# Passo 3: Exibir os Dados no Console
## Itere sobre a lista de pessoas e exiba as informações no console:
<pre>
    <code>
        <h3>
foreach (var pessoa in pessoas) {
    Console.WriteLine($"ID: {pessoa.Id}, Nome: {pessoa.Nome}, Email: {pessoa.Email}");
}
        </h3>
    </code>
</pre>

<pre>
    <code>
        <h3>
class Program {
    static void Main(string[] args) {
        using (var context = new CadastroPessoaContext()) {
            var pessoas = context.Pessoas.ToList();
            foreach (var pessoa in pessoas) {
                Console.WriteLine($"ID: {pessoa.Id}, Nome: {pessoa.Nome}, Email: {pessoa.Email}");
            }
        }
    }
}
        </h3>
    </code>
</pre>

# Explicação dos Passos
## ToList(): Este método executa a consulta e retorna os resultados como uma lista de objetos do tipo Pessoa.
## LINQ: O LINQ permite que você consulte o banco de dados usando a sintaxe C#. Você pode usar outros métodos, como Where, OrderBy, etc., para refinar as consultas.
## Console.WriteLine: Exibe as propriedades de cada objeto Pessoa no console.
# Dicas Extras
## Filtragem de Dados: Se você quiser filtrar os dados, pode usar o método Where. Exemplo:
<pre>
    <code>
        <h3>
var pessoas = context.Pessoas.Where(p => p.Nome.Contains("Maria")).ToList();
        </h3>
    </code>
</pre>

## Ordenação: Para ordenar os resultados, use o OrderBy:
<Pre>
    <code>
        <h3>
var pessoas = context.Pessoas.OrderBy(p => p.Nome).ToList();
        </h3>
    </code>
</Pre>

## Paginação: Se o banco de dados tiver muitos registros, considere usar Skip e Take para paginação.

# Passos Detalhados para Atualizar Dados no Banco de Dados
# 1. Preparar o Ambiente
## Certifique-se de que o projeto está configurado corretamente com o Entity Framework Core e que você já tem o modelo e o contexto do banco de dados prontos.

# 2. Recuperar o Registro a Ser Atualizado
## Primeiro, você precisa buscar o registro que deseja atualizar. Isso pode ser feito utilizando o método Find ou uma consulta LINQ para localizar o registro.
## Por exemplo, vamos supor que você queira corrigir o nome de uma pessoa na tabela Pessoas.
# Passo 1: Criar uma Instância do Contexto
<pre>
    <code>
        <h3>
using (var context = new CadastroPessoaContext()) {
    // A partir daqui, você pode buscar e atualizar os dados
}
        </h3>
    </code>
</pre>

# Passo 2: Buscar o Registro Específico
## Você pode buscar o registro pelo ID ou por outra propriedade. Exemplo buscando pelo Id:
<pre>
    <code>
        <h3>
var pessoa = context.Pessoas.Find(1); // Suponha que 1 é o ID do registro a ser corrigido
        </h3>
    </code>
</pre>

## Ou, se você quiser buscar por outro campo, como o nome:
<pre>
    <code>
        <h3>
var pessoa = context.Pessoas.FirstOrDefault(p => p.Nome == "Nome Incorreto");
        </h3>
    </code>
</pre>

# Passo 3: Verificar se o Registro Existe
## Sempre verifique se o registro foi encontrado antes de tentar atualizá-lo:
<pre>
    <code>
        <h3>
if (pessoa != null) {
    // O registro foi encontrado e você pode proceder com a atualização
} else {
    Console.WriteLine("Registro não encontrado.");
}
        </h3>
    </code>
</pre>

# 3. Atualizar o Registro
## Uma vez que você tenha o registro, pode modificar as propriedades que precisam ser corrigidas. Por exemplo, para corrigir o nome:
<pre>
    <code>
        <h3>
pessoa.Nome = "Nome Corrigido";
        </h3>
    </code>
</pre>

# 4. Salvar as Alterações no Banco de Dados
## Depois de alterar os dados, você precisa salvar as alterações no banco de dados:
<pre>
    <code>
        <h3>
context.SaveChanges();
        </h3>
    </code>
</pre>

#3 Aqui está o código completo para atualizar um registro:
<pre>
    <code>
        <h3>
class Program {
        static void Main(string[] args) {
            using (var context = new CadastroPessoaContext()) {
                var pessoa = context.Pessoas.FirstOrDefault(p => p.Nome == "Nome Incorreto");       
                if (pessoa != null) {
                    pessoa.Nome = "Nome Corrigido";
                    context.SaveChanges();
                    Console.WriteLine("Dados atualizados com sucesso!");
                } else {
                    Console.WriteLine("Registro não encontrado.");
                }
            }
        }
    }
}
        </h3>
    </code>
</pre>

# 5. Executar o Projeto
## Compile e execute o projeto.
## O código buscará o registro específico pelo nome "Nome Incorreto".
## Se o registro for encontrado, ele será atualizado com o novo nome "Nome Corrigido" e as alterações serão salvas no banco de dados.
## O console exibirá uma mensagem indicando se a atualização foi bem-sucedida ou se o registro não foi encontrado.

## Recuperar o Registro a Ser Excluído
## Primeiro, você precisa buscar o registro (usuário) que deseja excluir. Isso pode ser feito utilizando o método Find ou uma consulta LINQ * para localizar o registro específico.
# Passo 1: Criar uma Instância do Contexto
<pre>
    <Code>
        <h3>
using (var context = new CadastroPessoaContext()) {
    // A partir daqui, você pode buscar e excluir os dados
}
        </h3>
    </Code>
</pre>

# Passo 2: Buscar o Registro Específico
## Você pode buscar o registro pelo ID ou por outro critério. Exemplo buscando pelo Id:
<pre>
    <code>
        <h3>
var pessoa = context.Pessoas.Find(1); // Suponha que 1 é o ID do usuário a ser excluído.
        </h3>
    </code>
</pre>

## Ou, se você quiser buscar por outro campo, como o nome:
<pre>
    <code>
        <h3>
var pessoa = context.Pessoas.FirstOrDefault(p => p.Nome == "Maria Silva");
        </h3>
    </code>
</pre>

# Passo 3: Verificar se o Registro Existe
## Antes de tentar excluir o registro, verifique se ele foi encontrado:
<pre>
    <code>
        <h3>
if (pessoa != null) {
    // O registro foi encontrado e você pode proceder com a exclusão
} else {
    Console.WriteLine("Usuário não encontrado.");
}
        </h3>
    </code>
</pre>

# Excluir o Registro
## Se o registro foi encontrado, você pode excluí-lo usando o método Remove:
<pre>
    <code>
        <h3>
context.Pessoas.Remove(pessoa);
        </h3>
    </code>
</pre>

# Salvar as Alterações no Banco de Dados
## Após remover o registro, você deve salvar as alterações para que a exclusão seja refletida no banco de dados:
<pre>
    <code>
        <h3>
        context.SaveChanges();
        </h3>
    </code>
</pre>

## Aqui está o código completo para excluir um registro:
<pre>
    <code>
        <h3>
class Program {
static void Main(string[] args) {
    using (var context = new CadastroPessoaContext()) {
        var pessoa = context.Pessoas.FirstOrDefault(p => p.Nome == "Maria Silva");

        if (pessoa != null) {
            context.Pessoas.Remove(pessoa);
            context.SaveChanges();
            Console.WriteLine("Usuário excluído com sucesso!");
        } else {
            Console.WriteLine("Usuário não encontrado.");
        }
    }
}
        </h3>
    </code>
</pre>

# Compile e execute o projeto.
## O código buscará o registro específico pelo nome "Maria Silva".
## Se o registro for encontrado, ele será excluído e as alterações serão salvas no banco de dados.
## O console exibirá uma mensagem indicando se a exclusão foi bem-sucedida ou se o usuário não foi encontrado.
