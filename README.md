# Bússola · Despacho inteligente de cana (COA)

Painel que diz **para qual unidade mandar cada caminhão de cana**: Iturama, Limeira do Oeste ou Carneirinho. Ele também prevê o estoque de cada unidade em **voltas** e quanto tempo a cana dura na moagem (t/min).

Nasceu de um caso real: as unidades perto estavam cheias, o caminhão foi mandado para uma mais longe, e lá a moenda não tinha como moer.

## O que tem

- **Visão geral:** caminhões quase cheios nas frentes (com destino previsto), turno atual, KPIs com mini-gráfico, cartão de cada unidade (voltas com faixa mín/máx, moagem t/min, autonomia, fila, previsão), mapa ao vivo com os caminhões, feed de eventos, balanço corte × moagem e últimos despachos.
- **Sugestões:** central que olha o sistema a cada segundo e diz o que fazer, com o custo de fazer e de não fazer:
  - *unidade vai ficar sem cana* → quem pode socorrer (caminhões na estrada, na fila de outra unidade ou quase cheios nas frentes), hora de chegada, diesel a mais e minutos de moenda parada evitados;
  - *moenda parada com caminhões esperando* → quantos compensa tirar da fila e para onde, e quando compensa esperar;
  - *caminhão indo para o lugar errado* (o destino piorou depois que saiu) → desvio na estrada;
  - *frente sem caminhão* → remanejar vazio de outra frente;
  - *unidade vai passar do máximo* → aviso e sugestão de reduzir o corte;
  - *rotas que não compensam* → fazenda × unidade que custa muito mais que a melhor opção, quantas vezes aconteceu em 24h e a partir de qual fila ela passa a valer.
  Cada sugestão traz a **conta passo a passo** ("Ver a conta"): estoque, consumo da moenda em t/min, quando chegam os próximos caminhões, tempo ficando × indo, diferença de tempo, diesel em litros e reais, falta de cana evitada e o resultado: compensa ou não compensa.
  Cada sugestão tem botão **Aplicar** (muda a simulação) e há um modo automático acima de um ganho mínimo.
- **Frota & frentes:** 101 rodotrens próprios divididos pelas 8 frentes de serviço, cada um com frota, placa, modelo e capacidade. Cada caminhão tem 3 motoristas, um por turno (A 07h–15h, B 15h–23h, C 23h–07h). Cada frente tem suas colhedoras, ritmo em t/h, o caminhão que está carregando (% cheio e quando enche), a fila de vazios e quem está voltando. Se a frota da frente estiver toda na rua, entra um terceiro. Tabela com filtro por frente, situação, frota, placa ou motorista.
- **Fichas (toque em qualquer coisa):** caminhão (motorista do turno, frente, carga, destino, chegada, diesel da viagem), frente (colhedoras, carregamento, destino previsto, distância, tempo e diesel até cada unidade) e usina (fila e quem está a caminho). Funciona no mapa 2D, no 3D e nas tabelas.
- **Despacho:** escolha a frente e a carga para receber o destino recomendado, o ranking das unidades com o custo de cada uma e o que a regra atual faria.
- **Motoristas & turnos:** viagens, toneladas, ciclo médio, fila média, diesel e t/h no período (últimas 24h, turno, dia de safra, dia anterior). Toneladas por hora com a cor do turno, comparação A × B × C, fila média por unidade e turno (onde o tempo se perde), destaques e ranking de motoristas com ficha individual (viagens de hoje, últimas viagens, colegas do mesmo caminhão).
- **Calculadora de rota:** para cada fazenda, compara Iturama, Limeira e Carneirinho: distância, tempo de ida carregado e volta vazio, fila prevista, descarga, ciclo completo, diesel da ida e da volta (consumos diferentes), custo do diesel, R$ e litros por tonelada, CO₂, viagens por turno e custo da hora do caminhão. Projeta o diesel por dia e na safra e tem uma matriz de todas as fazendas × unidades em R$/t.
- **Predição:** estoque das últimas 6 horas e previsão das próximas 6 horas por unidade, com quando enche e quando falta cana.
- **Mapa 3D:** usinas com pilha de estoque (anel amarelo = mínimo, vermelho = máximo), frentes e caminhões andando. Toque em qualquer coisa para ver os detalhes.
- **Comparativo:** Bússola × regra atual rodando com a mesma cana e as mesmas paradas.
- **Histórico:** tabela de despachos com filtros.
- **Configurações:** moagem, toneladas por volta, mínimo/máximo, custos, botão para parar uma moenda e o cenário do caso real.
- **Modo TV** (visão geral, frota, motoristas, predição, 3D e comparativo girando a cada 15 s), **tema escuro** e simulação ao vivo em **1× / 60× / 300×**.

## As contas

- **Voltas** = estoque (t) ÷ toneladas por volta (ajustável por unidade).
- **Autonomia** = estoque (t) ÷ moagem (t/min).
- **Previsão do estoque:** pega o estoque de agora, soma os caminhões a caminho (pela hora de chegada), depois soma a média de cana que chegou nas últimas 2 h e tira a moagem. Paradas programadas e paradas em andamento zeram a moagem até a volta prevista.
- **Fila prevista** = (estoque na chegada − estoque que cabe no pátio sem fila) ÷ moagem.
- **Custo de cada destino** = diesel (ida e volta) + hora do caminhão (viagem + fila + espera de moenda parada) + ATR perdido + penalidade por passar do máximo − bônus se a carga evita moenda sem cana.
- O caminhão só sai da unidade mais perto se a economia passar do limiar (padrão R$ 150), se a moenda dela estiver parada ou se o pátio dela for passar do máximo.

> Os números de fábrica (moagem, t por volta, distâncias, custos) são aproximados. Ajuste em **Configurações** com os dados reais do COA.

## Publicar no GitHub Pages

1. Crie um repositório (ex.: `bussola-coa`) e envie o `index.html` e este `README.md`.
2. Vá em **Settings → Pages → Branch: main / root → Save**.
3. Acesse `https://SEU-USUARIO.github.io/bussola-coa/`.

É um arquivo único. O 3D baixa o Three.js da internet (jsDelivr) e o resto funciona offline.
