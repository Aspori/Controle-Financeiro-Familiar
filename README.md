# Finanças da Família

Site de controle financeiro feito para uso da família, rodando num computador de casa e acessado pelo navegador por qualquer aparelho da rede local.

Projeto pessoal, criado também como estudo de back-end, front-end e banco de dados.

> **Status:** em desenvolvimento. Veja o [roteiro](#roteiro) para saber o que já está pronto.

---

## O que o site faz

Funcionalidades do MVP (versão mínima):

- Cadastrar entradas (salário, renda extra) e saídas (mercado, contas, lazer)
- Organizar por categorias
- Registrar quem da família fez cada lançamento
- Ver a lista de lançamentos de cada mês
- Ver o resumo do mês: total de entradas, total de saídas e saldo
- Login com senha para cada pessoa

Planejado para depois do MVP:

- Filtros por categoria e por pessoa
- Gráficos (gastos por categoria, comparativo mês a mês)
- Orçamento por categoria e alertas
- Contas fixas e recorrentes
- Exportar para CSV

---

## Tecnologias

| Parte | Tecnologia |
|---|---|
| Back-end | Python + Flask |
| Banco de dados | SQLite |
| Front-end | HTML, CSS e JavaScript (templates Jinja2) |
| Gráficos | Chart.js (arquivo local, para funcionar sem internet) |
| Testes | pytest |
| Servidor para uso diário | Waitress |

---

## Estrutura do projeto

```
financas-familia/
├── app.py              # rotas do Flask e lógica principal
├── requirements.txt    # bibliotecas do projeto
├── .gitignore
├── README.md
├── templates/          # telas em HTML (Jinja2)
│   ├── base.html       # layout comum a todas as telas
│   ├── index.html      # resumo do mês
│   └── novo.html       # formulário de novo lançamento
└── static/             # CSS, JavaScript e imagens
    └── style.css
```

Arquivos criados na execução e que **não** vão para o Git: `financas.db` (banco de dados), `venv/` (ambiente virtual) e `.env` (segredos).

---

## Como instalar

Pré-requisitos: [Python 3.10+](https://www.python.org/downloads/) e [Git](https://git-scm.com/).

1. Clone o repositório e entre na pasta:

   ```
   git clone https://github.com/SEU_USUARIO/financas-familia.git
   cd financas-familia
   ```

2. Crie o ambiente virtual:

   ```
   python -m venv venv
   ```

3. Ative o ambiente virtual (o `(venv)` deve aparecer no início da linha do terminal):

   ```
   venv\Scripts\Activate.ps1      # Windows (PowerShell)
   venv\Scripts\activate.bat      # Windows (CMD)
   source venv/bin/activate       # Mac/Linux
   ```

4. Instale as dependências:

   ```
   pip install -r requirements.txt
   ```

5. Crie o arquivo `.env` na raiz do projeto com uma chave secreta sua:

   ```
   SECRET_KEY=troque-por-um-texto-longo-e-aleatorio
   ```

---

## Como rodar

### No próprio computador (teste)

```
flask run
```

Abra `http://localhost:5000` no navegador.

### Para a família acessar pela rede de casa

1. No computador que vai ser o servidor, rode:

   ```
   flask run --host=0.0.0.0 --port=5000
   ```

2. Descubra o IP do servidor com `ipconfig` (Windows) ou `ip a` (Linux). Procure o "Endereço IPv4", algo como `192.168.0.10`.
3. Na primeira vez, permita o Python no firewall do Windows em **rede privada**.
4. Nos outros aparelhos, conectados ao **mesmo Wi-Fi**, abra `http://IP-DO-SERVIDOR:5000` (exemplo: `http://192.168.0.10:5000`).

Para uso no dia a dia, prefira o Waitress em vez do servidor de desenvolvimento do Flask:

```
pip install waitress
waitress-serve --host=0.0.0.0 --port=5000 app:app
```

Dicas para deixar estável:

- Reserve o IP do servidor no roteador (procure "Reserva de DHCP"), para o endereço não mudar.
- Configure o computador para não entrar em suspensão.
- Crie um atalho de inicialização para o site subir junto com o computador.

---

## Backup

O banco de dados é um único arquivo (`financas.db`). Faça cópia dele com frequência:

- Copie o arquivo para uma pasta `backup/` com a data no nome (ex.: `financas-2026-10-05.db`)
- Guarde uma cópia fora do computador (pendrive ou nuvem privada)
- Teste restaurar um backup de vez em quando

---

## Segurança

Este projeto foi feito para uso **apenas dentro da rede de casa**.

- **Não abra portas no roteador** (port forwarding) para deixar o site acessível pela internet
- Senhas são guardadas com hash, nunca em texto puro
- Mantenha o modo debug desligado ao usar na rede
- Mantenha o repositório do GitHub **privado** e nunca suba o `financas.db` nem o `.env`

---

## Testes

```
pytest
```

Os testes usam um banco separado, nunca o banco real da família.

---

## Roteiro

- [x] Planejamento e desenho das telas
- [ ] Ambiente, Git e servidor de teste
- [ ] Banco de dados (tabelas `usuarios`, `categorias`, `lancamentos`)
- [ ] Back-end: cadastro, lista, edição e exclusão
- [ ] Resumo mensal
- [ ] Login e proteção das rotas
- [ ] Front-end: layout base, CSS e versão para celular
- [ ] Gráficos
- [ ] Testes
- [ ] Backup automático
- [ ] Site rodando na rede da família

(Marque cada item conforme for terminando.)

---

## Anotações de estudo

Espaço para registrar o que aprendi em cada fase.

- **Banco de dados:** _(ex.: por que guardar dinheiro em centavos, normalização)_
- **Back-end:** _(ex.: rotas, sessões, validação)_
- **Front-end:** _(ex.: Flexbox, Grid, responsividade)_
- **Rede:** _(ex.: IP local, firewall, DHCP)_

---

## Autor

Feito por **Vinicius**.