---
layout: post
title: Corrigir suporte Python3 para MacVim 9.0
categories: Vim
description: Corrigir suporte Python3 para MacVim 9.0修复 MacVim 9.0 的 Python3 支持
keywords: MacVim, Python3
---

Acabei de atualizar para a versão mais recente do MacVim 9.0 há dois dias e não encontrei nenhum problema na edição diária e na edição de texto, até que movi o plug-in hoje.

## problema encontrado

Eu vi um plug-in do Vim interessante esta manhã, instalei e experimentei, mas não me pareceu muito prático, então apaguei a configuração e planejei executá-lo `:PlugClean ` para limpá dois plug-ins—— Além deste teste, há também o LeaderF.

LeaderF é um dos plug-ins que eu uso muito. Não expressei minha intenção de excluí-lo. O que aconteceu para o vim-plug pensar assim? Deve haver algum mal-entendido.

No meu arquivo _vimrc, adicionar o plug-in LeaderF é escrito assim:

```
if has('python') || has('python3')
    Plug 'Yggdroot/LeaderF', { 'do': ':LeaderfInstallCExtension' }
endif
```

Então eu abri uma janela do MacVim, tentei `:echo has('python')` e `:echo has('python3')`, a saída acabou sendo 0, não é de admirar...

## analisar problema

No começo, eu quero principalmente descobrir dois pontos:

1. A versão do MacVim que estou usando foi compilada com suporte a Python ativado?

    Executando na janela do MacVim `:version`, você pode ver `+python/dyn` e `+python3/dyn`, o que significa que o suporte a Python e Python3 está ativado ao mesmo tempo.

2. Eu tenho o Python instalado localmente?

    ```sh
    $ python
    zsh: command not found: python

    $ brew list | grep python
    python@3.10
    python@3.8
    python@3.9

    $ python3
    Python 3.9.12 (main, Mar 26 2022, 15:51:15)
    [Clang 13.1.6 (clang-1316.0.21.2)] on darwin
    Type "help", "copyright", "credits" or "license" for more information.
    >>>
    ```

    Você pode ver que instalei Python3 versões 3.8, 3.9 e 3.10 localmente. O padrão é 3.9 e o Python2 não está instalado

Não há nada de errado com isso, então continue procurando e tente executar as instruções do Python3 no MacVim:

```
:py3 import sys;
```

Como resultado, vários erros foram gerados:

```
E370: Não foi possível carregar a biblioteca /usr/local/Frameworks/Python.framework/Versions/3.10/Python：dlopen(/usr/local/Frameworks/Python.fram
ework/Versions/3.10/Python, 0x0009): tried: '/usr/local/Frameworks/Python.framework/Versions/3.10/Python' (no such fil
e), '/Library/Frameworks/Python.framework/Versions/3.10/Python' (no such file), '/System/Library/Frameworks/Python.fra
mework/Versions/3.10/Python' (no such file)
E263: Desculpe, este comando não está disponível, a biblioteca Python não pôde ser carregada。
```

O caminho do arquivo que ele está procurando não existe... Afinal, minha versão padrão é 3.9, então há apenas 3.9 e os diretórios atuais em /usr/local/Frameworks/Python.framework/Versions/, não 3.10.

Por que ele deixa a versão 3.9 configurada sem uso, então deve estar tão desesperado para encontrar a versão 3.10? Esta pergunta não será respondida por enquanto, e será deixada para o link de questionamento posterior. Agora, para o problema.。

## Resolva o problema

Depois de pesquisar a mensagem de erro acima na Internet, descobri que a biblioteca de suporte Python3 carregada dinamicamente pode ser especificada `pythonthreedll` definindo .

Além disso, também aprendi como alternar a versão padrão de várias versões do Python instaladas por meio do brew.

Portanto, este pequeno problema encontrou duas soluções:

1. Adicione a configuração em _vimrc para especificar o caminho da biblioteca de suporte do Python3 carregado dinamicamente, por exemplo:

    ```vim
    let &pythonthreedll='/usr/local/Frameworks/Python.framework/Versions/3.9/python'
    ```

2. Mude a versão Python3 padrão do sistema. Por exemplo, se o MacVim estiver procurando a versão 3.10 aqui, mudarei a versão padrão para a versão 3.10:

    ```sh
    brew unlink python@3.9
    brew link python@3.10
    ```

Foi verificado que os dois métodos acima podem resolver o problema e, finalmente, usei o segundo.

## Chegue ao fundo disso

Deixamos uma pergunta acima, por que o MacVim insiste em carregar a versão 3.10 da biblioteca de suporte do Python?

Primeiro `pythonthreedll` veja a descrição do documento de ajuda:

```
:h pythonthreedll
```

pode ser visto:

```
'pythonthreedll'	string	(default depends on the build)
			global
			{only available when compiled with the |+python3/dyn|
			feature}
	Specifies the name of the Python 3 shared library. The default is
	DYNAMIC_PYTHON3_DLL, which was specified at compile time.
	Environment variables are expanded |:set_env|.
	This option cannot be set from a |modeline| or in the |sandbox|, for
	security reasons.
```

Ou seja, o valor padrão é `DYNAMIC_PYTHON3_DLL` o valor entendi, significa que se não for especificado no arquivo de configuração, ele será carregado conforme especificado em tempo de compilação.

Ao compilar `DYNAMIC_PYTHON3_DLL`，, podemos encontrá-lo no warehouse.github [.github/worflows/ci-macvim.yaml](https://github.com/macvim-dev/macvim/blob/master/.github/workflows/ci-macvim.yaml) macvim.yaml oficial do MacVim , o conteúdo principal:

```yaml
...

vi_cv_dll_name_python3: /usr/local/Frameworks/Python.framework/Versions/3.10/Python 
# Make sure to keep src/MacVim/vimrc synced with the Python version here for the Python DLL detection logic.

...

grep -q -- "-DDYNAMIC_PYTHON3_DLL=\\\\\"${vi_cv_dll_name_python3}\\\\\"" src/auto/config.mk

...
```

Até agora o caso foi resolvido.

## Bibliografia

- <https://www.jianshu.com/p/18f06d12348c>
