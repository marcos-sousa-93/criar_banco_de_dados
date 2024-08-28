# criar_banco_de_dados
Criando banco de dados em C#
1 Instalar os Pacotes Necessários:
No Gerenciador de Pacotes NuGet, adicione os seguintes pacotes ao seu projeto:

PM> Install-Package Microsoft.EntityFrameworkCore
PM> Install-Package Microsoft.EntityFrameworkCore.SqlServer
PM> Install-Package Microsoft.EntityFrameworkCore.Tools

2 Criar o Modelo (Classes):
Crie classes que representem as tabelas do banco de dados. Por exemplo:

public class Pessoa
{
    public int Id { get; set; }
    public string Nome { get; set; }
    public string Email { get; set; }
}

3 Criar o Contexto do Banco de Dados:
Crie uma classe que herda de DbContext e define as DbSet para as entidades:

public class CadastroPessoaContext : DbContext
{
    public DbSet<Pessoa> Pessoas { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseSqlServer(@"Server=(localdb)\mssqllocaldb;Database=CadastroPessoaDB;Trusted_Connection=True;");
    }
}

4 Criar as Migrations:
No Gerenciador de Pacotes NuGet, rode o comando para criar a migration inicial:

PM> Add-Migration InitialCreate

5 Atualizar o Banco de Dados:
Aplique a migration para criar o banco de dados:

PM> Update-Database
