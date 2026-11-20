# Keyring

O chaveiro das contas: guarda as chaves de cada conta de delivery e mostra com quem cada uma está. App pessoal para controlar contas de plataformas de delivery (Grubhub, Amazon Flex, DoorDash…) alugadas para clientes: quem está com cada conta, quanto entrou na semana, quanto falta e quem precisa ser cobrado no WhatsApp.

**Abrir:** https://gustavodga.github.io/KEYRING/
No iPhone: abra no Safari, toque em Compartilhar e depois em "Adicionar à Tela de Início".

## Telas

- **Semana:** anel do quanto já entrou, faixa dos 7 dias com o status de cada cobrança, atrasos de semanas anteriores à parte, registrar pagamento e cobrar no WhatsApp.
- **Contas:** cartões por conta com a cor da plataforma, aluguel, reajuste, encerramento e troca de cliente.
- **Clientes:** saldo, pendências, promessas, histórico em linha do tempo e resumo pelo WhatsApp.
- **Painel:** ocupação da frota, quanto rende por semana, quanto fica parado, recebido por semana, idade do atraso, quem paga em dia, rendimento por conta e resumo do ano para o contador.
- **Bônus:** subsídios das plataformas com divisão editável (padrão 70% cliente / 30% você) e etapas aguardando → recebido → repassado.

## Onde ficam os dados

No próprio aparelho (`localStorage`, chave `keyring-v1`). Não há servidor nem login.
Use **Ajustes → Copiar backup** de vez em quando e guarde o texto numa nota ou e-mail. Para levar os dados a outro aparelho, use **Restaurar backup** lá.

## Regras

- Datas no fuso America/Los_Angeles; semana de segunda a domingo.
- Cobranças são geradas até o fim da semana atual. O id de cada cobrança é `vínculo-AAAAMMDD`, então abrir de novo nunca duplica.
- Uma conta só pode ter um aluguel ativo. Encerrar mantém as pendências até o último dia; cobranças depois dele sem pagamento são removidas.
- Reajuste vale para vencimentos a partir da data escolhida; cobranças pagas nunca mudam de valor.
- Promessa de pagamento não muda o vencimento; no dia combinado a cobrança volta ao topo.
- Valores guardados em centavos (inteiros).

## Estrutura

```
index.html           o app inteiro (HTML, CSS e JavaScript num arquivo só)
manifest.json        nome, cores e ícones para instalar na tela inicial
sw.js                cache para abrir sem internet
icon-*.png           ícones
.nojekyll            publica no GitHub Pages sem processamento
```

Para editar, mexa em `index.html` e faça commit: o GitHub Pages publica sozinho em cerca de um minuto. Ao trocar arquivos além do `index.html`, aumente a versão em `CACHE` no `sw.js`.

Quando aberto como artifact do claude.ai, o mesmo arquivo usa o armazenamento da conta do claude.ai em vez do aparelho.
