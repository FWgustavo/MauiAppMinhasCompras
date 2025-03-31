# AppMinhasCompras 🛒📱

## 📌 Visão Geral do Projeto

O AppMinhasCompras é um aplicativo móvel multiplataforma desenvolvido em .NET MAUI para gerenciar listas de compras e controlar gastos pessoais.



![Demonstração do App](https://i.gifer.com/X5NZ.gif)

## 📸 Capturas de Tela

> IMPORTANTE: Substitua pelas screenshots reais do seu aplicativo
![Tela Inicial](repos/MauiAppMinhasCompras/MauiAppMinhasCompras/Resources/Images/telainicial.png)
![Lista de Compras](/caminho/para/lista-compras.png)
![Adicionar Compra](/caminho/para/adicionar-compra.png)

## 💻 Tecnologias Utilizadas

- **Linguagem**: C#
- **Framework**: .NET MAUI
- **Padrão Arquitetural**: MVVM
- **Persistência**: SQLite

## 🗂️ Estrutura do Projeto

```
MauiAppMinhasCompras/
│
├── Models/
│   └── Produto.cs
│
├── Views/
│   ├── MainPage.xaml
│   └── ProdutoPage.xaml
│
├── ViewModels/
│   └── ProdutoViewModel.cs
│
└── Services/
    └── ProdutoService.cs
```

## 🔍 Detalhamento do Código-Fonte

### Model: Produto.cs
```csharp
// Utilização da biblioteca SQLite para persistência de dados
using SQLite;

// Definição do namespace para o modelo de Produto
namespace MauiAppMinhasCompras.Models
{
    // Classe Produto representa um item em um sistema de compras
    public class Produto 
    {
        // Identificador único do produto
        // Configurado como chave primária e com incremento automático
        [PrimaryKey, AutoIncrement]
        public int Id { get; set; }

        // Propriedade para armazenar a descrição do produto
        // Implementa validação para impedir descrições nulas
        public string Descrição 
        { 
            get; 
            set 
            {
                // Verifica se o valor da descrição é nulo
                if (value == null)
                {
                    // Lança uma exceção caso a descrição esteja vazia
                    throw new Exception("Por favor, preencha a descrição");
                }
                // Atribui o valor à descrição
                _descrição = value;
            } 
        }

        // Propriedade para armazenar a quantidade do produto
        public double Quantidade { get; set; }

        // Propriedade para armazenar o preço do produto
        public double Preço { get; set; }

        // Propriedade calculada para o valor total (quantidade * preço)
        public double Total { get => Quantidade * Preço; }
    } // Fecha classe Produto
} // Fecha namespace
```

### ViewModel: ProdutoViewModel.cs
```csharp
public class ProdutoViewModel : INotifyPropertyChanged
{
    private ObservableCollection<Produto> _produtos;
    public ObservableCollection<Produto> Produtos 
    {
        get => _produtos;
        set 
        {
            _produtos = value;
            OnPropertyChanged(nameof(Produtos));
        }
    }

    public ICommand AdicionarProdutoCommand { get; }
    public ICommand RemoverProdutoCommand { get; }
}
```

### Service: ProdutoService.cs
```csharp
public class ProdutoService
{
    private readonly SQLiteConnection _database;

    public ProdutoService(string dbPath)
    {
        _database = new SQLiteConnection(dbPath);
        _database.CreateTable<Produto>();
    }

    public List<Produto> ObterTodosProdutos()
    {
        return _database.Table<Produto>().ToList();
    }

    public void AdicionarProduto(Produto produto)
    {
        _database.Insert(produto);
    }
}
```

## 🚀 Funcionalidades

- [x] Cadastro de produtos
- [x] Cálculo automático de total
- [x] Persistência local de dados
- [ ] Exportação de lista de compras
- [ ] Tema escuro

## 🔧 Instalação e Configuração

### Pré-requisitos
- Visual Studio 2022
- .NET 7 SDK
- Carga de trabalho .NET MAUI

### Passos de Instalação
1. Clone o repositório
2. Abra no Visual Studio
3. Restaure pacotes NuGet
4. Compile o projeto
5. Execute no dispositivo/emulador

## 🤝 Como Contribuir

1. Faça um fork do projeto
2. Crie branch para sua feature
3. Commit suas mudanças
4. Abra um Pull Request

## 📋 Próximas Etapas

- [ ] Implementar tema escuro
- [ ] Adicionar gráficos de gastos
- [ ] Criar sincronização em nuvem

## 👥 Contato

- Desenvolvedor: Gustavo Merschbacher
- GitHub: [@FWgustavo](https://github.com/FWgustavo)

## 📄 Licença

[Especificar licença do projeto]
```

Observações importantes:

1. Esta é uma documentação modelo que precisa ser personalizada com:
   - Screenshots reais do aplicativo
   - GIF de demonstração
   - Código-fonte exato do seu repositório
   - Detalhes específicos da sua implementação

2. Recomendo substituir os placeholders com informações reais do seu projeto.

Gostaria que eu detalhe alguma seção específica ou faça alguma modificação?
