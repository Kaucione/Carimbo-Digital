# Assinatura Automática de PDFs com Carimbo

Este repositório contém um script em Python para adicionar automaticamente um carimbo de autenticação a documentos PDF. O carimbo inclui informações institucionais, servidor responsável, data/hora de Brasília e uma logo institucional em base64.

## Funcionalidades

* Seleção de servidor pré-cadastrado ou inserção manual de dados.
* Geração de carimbo em PDF com moldura e logo.
* Inclusão da data e hora de Brasília (fuso horário atualizado via `pytz`).
* Aplicação do carimbo em todas as páginas dos PDFs enviados.
* Exportação dos arquivos assinados com prefixo `assinado_`.

## Requisitos

Instale as dependências com:

```bash
pip install pymupdf reportlab pytz
```

## Uso

1. Execute o script em ambiente compatível (ex.: Google Colab, Jupyter Notebook ou local).
2. Escolha um servidor do banco local ou insira manualmente:

   * Nome
   * Cargo
   * Matrícula
3. Faça upload do(s) PDF(s) a serem assinados.
4. O script aplicará o carimbo em todas as páginas.
5. Os arquivos resultantes serão gerados no formato:

   ```
   assinado_nomeoriginal.pdf
   ```

## Estrutura do Carimbo

O carimbo contém:

```
ESTADO DE ALAGOAS
SECRETARIA DE ESTADO
CNPJ:
SETOR

ESTE DOCUMENTO AUTENTICADO CONFERE COM O ORIGINAL.

[NOME DO SERVIDOR]
[Cargo do Servidor]
Matrícula: XXXXX
Maceió, DD/MM/AAAA HH:MM:SS
```

Além do texto, o carimbo possui:

* Logo centralizada (em base64).
* Moldura retangular.

## Exemplo de Saída

Entrada:

```
documento.pdf
```

Saída:

```
assinado_documento.pdf
```

## Observações

* O campo `logo_base64` deve conter a imagem em formato base64.
* Os servidores podem ser cadastrados e mantidos no dicionário `servidores` no início do código.
* A posição e tamanho do carimbo podem ser ajustados no trecho:

  ```python
  rect = fitz.Rect(x, y, x + carimbo_w, y + carimbo_h)
  ```

