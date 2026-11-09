# Desafio DevOps — A Esteira de Entrega Profissional

**Aluna:** Távine de Andrade Onofre

## Conteúdo
- `index.html`, `sobre.html` e `contato.html`: páginas do site.
- `style.css`: estilos.
- `assets/logo.svg`: imagem do site.
- `.github/workflows/deploy.yml`: pipeline de build, auditoria e deploy.
- `dist/`: criada automaticamente pelo GitHub Actions (não precisa criar manualmente).

## Como testar localmente
Abra `index.html` no navegador. Teste os links do menu e confira a imagem.

## Como publicar no GitHub
1. Crie um repositório vazio no GitHub com o nome `desafio-devops-tavine` (ou outro nome).
2. Extraia este ZIP e abra a pasta no VS Code.
3. Abra o terminal nessa pasta e execute:

```bash
git init
git branch -M main
git add .
git commit -m "Adiciona site e esteira DevOps"
git remote add origin https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git
git push -u origin main
```

Troque a URL pelo endereço real do seu repositório.
4. No GitHub, abra **Settings > Pages** e, em **Build and deployment**, selecione **GitHub Actions**.
5. Abra a aba **Actions** e acompanhe a execução. O job `build` deve organizar `dist`, executar a auditoria e enviar o pacote; depois o job `deploy` publica o site.

## Parte 4 — provocar a falha (faça depois da primeira publicação)
1. No VS Code, renomeie `sobre.html` para `quem-somos.html`.
2. Para provocar a falha pedida, deixe temporariamente no `deploy.yml` esta linha na auditoria:

```yaml
test -f dist/sobre.html
```

3. Altere também o link do menu em `index.html` para `quem-somos.html`.
4. Envie a alteração:

```bash
git add .
git commit -m "Provoca falha na auditoria"
git push
```

5. Em **GitHub > Actions**, abra a execução vermelha e o passo **Auditoria de Qualidade**. Tire um print real do erro que indica que `dist/sobre.html` não foi encontrado.

## Correção final
Substitua a verificação antiga pela nova:

```yaml
test -f dist/quem-somos.html
```

A auditoria final também precisa verificar `index.html` e `contato.html`. O workflow entregue neste ZIP já está na versão corrigida, usando `quem-somos.html`; para reproduzir a falha, faça a alteração temporária descrita acima e depois volte à versão corrigida.

Envie a correção:

```bash
git add .
git commit -m "Corrige auditoria de qualidade"
git push
```

Confirme que o GitHub Actions ficou verde e tire um print real da execução concluída.

## Observação
O repositório, o push e as capturas de tela precisam ser feitos na sua conta do GitHub. Não é possível gerar prints verdadeiros de uma execução sem acesso ao seu repositório. O workflow final deste pacote está preparado para publicar pelo GitHub Pages.
