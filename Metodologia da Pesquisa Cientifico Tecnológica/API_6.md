## Meu Sexto API  📚

#### Em 2024-1 (API 6)
Trabalhamos no projeto da API do sexto semestre com a empresa Imagem como parceira. [GitHub do projeto.](https://github.com/GroupHextech/HEXTECH-API6sem)<br> 


![image](https://github.com/HelenAlevato/Portfolio-Banco-de-Dados/assets/61571753/7cba775b-d4d4-4e35-8a35-50185c46f4e1)


- **Nome do Grupo:** HexTech
- **Nome do Software:**  HexAnalytics
- **Visão do Produto:** Este projeto visa desenvolver uma aplicação de análise de sentimento, com bons insights
     
 - **Objetivo do Produto:** 
	 - O objetivo é criar uma plataforma que entenda o que os clientes sentem através de avaliações online das lojas Americanas num determinado período, usando inteligência artificial para análise dos sentimentos, armazenar dados e mostrar tudo através de mapa de calor e gráficos. Assim, a empresa Imagem pode ver como os clientes se sentem em diferentes lugares e adaptar suas estratégias de marketing e atendimento. Com isso, podem tomar decisões melhores para melhorar a experiência do cliente e se conectar de forma mais forte com eles.
  
- **Problema (Desafio):** 

	- O problema identificado é a necessidade de entender profundamente o sentimento dos clientes de uma base de dados escolhida pelo grupo. O desafio de coletar e interpretar uma grande quantidade de avaliações online para obter insights sobre a satisfação e as expectativas dos consumidores. A falta de uma plataforma que integre análise de sentimentos é o principal problema.

- **Proposta:**
	- A proposta da equipe HexTech é desenvolver uma aplicação que aborde os desafios identificados anteriormente, visando oferecer uma solução completa para compreender e gerenciar os sentimentos dos clientes. O sistema proposto incluirá recursos de cadastro e login, diferenciando-se entre usuários administrativos e regulares, garantindo assim a segurança e privacidade dos dados conforme as leis de proteção de dados, como a LGPD. A tela principal será um dashboard fornecerão insights detalhados e relatórios personalizados sobre tendências de sentimentos e comparações históricas. A segunda tela principal será um mapa interativo, permitindo uma visualização geolocalizada dos sentimentos dos clientes.
	

#### Tecnologias Utilizadas 🛠
- Front-end: CSS, HTML, JavaScript, React, MUI, Visual Studio Code
- Back-end: Python, Flesk, Visual Studio Code
- Banco de Dados: Mongodb compass

## Contribuições Pessoais 👩
Nesse trabalho fiquei como Team Dev, responsável pela parte de front-end. 

**Desenvolvimento:** 
<details>
  <summary>Gráfico por gênero do dashboard</summary>
	
	O componente GenderPieChart faz um gráfico de pizza que exibe a distribuição de gêneros (Homens e Mulheres) 
 	com base em dados obtidos de um serviço, utilizando a biblioteca @nivo/pie para renderização e useEffect para 
  	buscar dados quando os filtros mudam.
  
  ```javascript

import { ResponsivePie } from "@nivo/pie";
import { tokens } from "../../theme";
import { useTheme } from "@mui/material";
import { useState, useEffect } from "react";
import { getGender } from "../../services/SalesService";

const GenderPieChart = ({filter}) => {
  const theme = useTheme();
  const colors = tokens(theme.palette.mode);
  const [genderData, setGenderData] = useState([]);

  useEffect(() => {
    async function handleGenderData() {
      try {
        const data = await getGender(filter.states, filter.regions, filter.feeling);
        setGenderData(data);
      } catch (error) {
        console.error("Error fetching genders:", error.message);
      }
    }

    handleGenderData();
  }, [filter]);

  if (genderData?.length)
    return (
      <ResponsivePie
        data={[
          {
            id: genderData[1]?._id ?? 'F',
            value: genderData[1]?.count ?? 0,
            label: "Mulheres",
          },
          {
            id: genderData[0]?._id ?? 'M',
            value: genderData[0]?.count ?? 0,
            label: "Homens",
          },
        ]}
        theme={{
          tooltip: {
            container: {
              background: "#fff", // cor de fundo do tooltip
              color: "#000", // cor do texto do tooltip
            },
          },
          axis: {
            domain: {
              line: {
                stroke: colors.grey[100],
              },
            },
            legend: {
              text: {
                fill: colors.grey[100],
              },
            },
            ticks: {
              line: {
                stroke: colors.grey[100],
                strokeWidth: 1,
              },
              text: {
                fill: colors.grey[100],
              },
            },
          },
          legends: {
            text: {
              fill: colors.grey[100],
            },
          },
        }}
        margin={{ top: 40, right: 80, bottom: 80, left: 80 }}
        innerRadius={0.5}
        padAngle={0.7}
        cornerRadius={3}
        activeOuterRadiusOffset={8}
        colors={{ scheme: 'category10' }}
        borderColor={{
          from: "color",
          modifiers: [["darker", 0.2]],
        }}
        arcLinkLabelsSkipAngle={10}
        arcLinkLabelsTextColor={colors.grey[100]}
        arcLinkLabelsThickness={2}
        arcLinkLabelsColor={{ from: "color" }}
        enableArcLabels={false}
        arcLabelsRadiusOffset={0.4}
        arcLabelsSkipAngle={7}
        arcLabelsTextColor={{
          from: "color",
          modifiers: [["darker", 2]],
        }}
        defs={[
          {
            id: "dots",
            type: "patternDots",
            background: "inherit",
            color: "rgba(255, 255, 255, 0.3)",
            size: 4,
            padding: 1,
            stagger: true,
          },
          {
            id: "lines",
            type: "patternLines",
            background: "inherit",
            color: "rgba(255, 255, 255, 0.3)",
            rotation: -45,
            lineWidth: 6,
            spacing: 10,
          },
        ]}
        legends={[
          {
            anchor: "bottom",
            direction: "row",
            justify: false,
            translateX: 0,
            translateY: 56,
            itemsSpacing: 0,
            itemWidth: 100,
            itemHeight: 18,
            itemTextColor: "#999",
            itemDirection: "left-to-right",
            itemOpacity: 1,
            symbolSize: 18,
            symbolShape: "circle",
            effects: [
              {
                on: "hover",
                style: {
                  itemTextColor: "#000",
                },
              },
            ],
          },
        ]}
      />
    );
};

export default GenderPieChart;

 
  ```
</details>

<details>
  <summary>Gráfico quantidades de vendas por período do dia</summary>
	
	O componente desse Chart exibe um gráfico de barras mostrando as vendas por períodos do dia (manhã, tarde, noite). 
 	Ele busca os dados de vendas com base em filtros aplicados e usa useEffect para atualizar os dados sempre que os filtros mudam. 
  	O gráfico é renderizado usando @nivo/bar com estilos personalizados.
  
  ```javascript

import { useTheme } from "@mui/material";
import { tokens } from "../../theme";
import { useState, useEffect } from "react";
import { getSales } from "../../services/SalesService";
import { ResponsiveBarCanvas } from "@nivo/bar";

function determinarPeriodo(horario) {
  // Extrair apenas a parte do horário
  const horarioSplit = horario.split(" ")[1];
  const [hora, minuto, segundo] = horarioSplit.split(":").map(Number);

  // Determinar o período com base nas horas
  if (hora >= 6 && hora < 12) {
    return "Morning";
  } else if (hora >= 12 && hora < 18) {
    return "Afternoon";
  } else {
    return "Night";
  }
}

function agruparVendasPorPeriodo(dados) {
  const vendasPorPeriodo = {};

  // Iterando sobre cada item dos dados
  dados.forEach((item) => {
    // Criando uma chave no formato "YYYY-MM" para representar o período
    const periodo = determinarPeriodo(item._id);

    // Inicializando o contador de vendas para o período, se necessário
    if (!vendasPorPeriodo[periodo]) {
      vendasPorPeriodo[periodo] = 0;
    }

    // Incrementando o contador de vendas para o período
    vendasPorPeriodo[periodo] = vendasPorPeriodo[periodo] + item.count;
  });

  // Convertendo o objeto em um array de objetos para o BarChart
  const vendasPorPeriodoArray = Object.entries(vendasPorPeriodo).map(
    ([periodo, quantidade]) => ({
      periodo,
      qtde: quantidade,
    })
  );

  return vendasPorPeriodoArray;
}

export default function Chart({filter}) {
  const theme = useTheme();
  const colors = tokens(theme.palette.mode);

  const [salesData, setSalesData] = useState([]);

  useEffect(() => {
    async function handleSalesData() {
      try {
        const data = await getSales(filter.states, filter.regions, filter.feeling);
        setSalesData(agruparVendasPorPeriodo(data));
      } catch (error) {
        console.error("Error fetching sales:", error.message);
      }
    }

    handleSalesData();
  }, [filter]);

  if (salesData?.length) {
    return (
      <ResponsiveBarCanvas
        data={salesData}
        theme={{
          tooltip: {
            container: {
              background: "#fff", // cor de fundo do tooltip
              color: "#000", // cor do texto do tooltip
            },
          },
          axis: {
            domain: {
              line: {
                stroke: colors.grey[100],
              },
            },
            legend: {
              text: {
                fill: colors.grey[100],
              },
            },
            ticks: {
              line: {
                stroke: colors.grey[100],
                strokeWidth: 1,
              },
              text: {
                fill: colors.grey[100],
              },
            },
          },
          legends: {
            text: {
              fill: colors.grey[100],
            },
          },
        }}
        keys={["qtde"]}
        indexBy="periodo"
        margin={{ top: 30, right: 0, bottom: 30, left: 50 }}
        padding={0.3}
        valueScale={{ type: "linear" }}
        indexScale={{ type: "band", round: true }}
        colors={{ scheme: 'category10' }}
        enableLabel={false}
        enableTotals={true}
        labelSkipWidth={12}
        labelSkipHeight={12}
        labelTextColor={{ theme: 'grid.line.stroke' }}
        role="application"
        isFocusable={true}
      />
    );
  }
}

 
  ```
</details>

<details>
  <summary>Adiciona gráfico de vendas por período mensal</summary>
	
	O componente desse Chart exibe um gráfico de linhas (bump chart) mostrando a evolução dos sentimentos 
 	(positivo, neutro, negativo) ao longo do tempo. Ele busca os dados de sentimentos com base em filtros 
  	aplicados, formata esses dados e usa useEffect para atualizar o gráfico sempre que os filtros mudam. 
   	O gráfico é renderizado usando @nivo/bump com estilos personalizados.
  
  ```javascript

import { useTheme } from "@mui/material";
import { tokens } from "../../theme";
import { useState, useEffect } from "react";
// import { getSales } from "../../services/SalesService";
import { ResponsiveBump } from "@nivo/bump";
import { getFeelingByMonth } from "../../services/SalesService";

export default function Chart({ filter, selectedSentiment }) {
  const theme = useTheme();
  const colors = tokens(theme.palette.mode);
  const [feelingData, setFeelingData] = useState([]);

  const sentimentColors = {
    Positive: colors.greenAccent[500], // Verde
    Neutral: "#ffa927", // Amarelo
    Negative: "#E0115F", // Vermelho
  };

  useEffect(() => {
    async function handleGetData() {
      try {
        const data = await getFeelingByMonth(
          filter.states,
          filter.regions,
          filter.feeling
        );

        // Mapeando os dados recebidos e reestruturando para o formato esperado pelo Nivo Bump Chart
        const formattedData = Object.keys(data[0])
          .filter((key) => key !== "_id")
          .map((key) => ({
            id: key,
            data: data.map((item) => ({
              x: item._id,
              y: item[key],
            })),
          }));

        setFeelingData(formattedData);
      } catch (error) {
        console.error("Error fetching feeling:", error.message);
      }
    }

    handleGetData();
  }, [filter]);

  const filteredData = selectedSentiment
    ? feelingData.filter((data) => data.id === selectedSentiment)
    : feelingData;

  if (true) {
    return (
      <>
        <ResponsiveBump
          data={filteredData.map((serie) => ({
            ...serie,
            data: serie.data.map((point) => ({ ...point, y: -point.y }))
          }))}
          keys={["Positive", "Neutral", "Negative"]}
          indexBy="_id"
          // indexScale={{ type: 'band', round: true }}
          colors={(data) => sentimentColors[data.id]}
          xPadding={0.4}
          activeLineWidth={3}
          inactiveLineWidth={0}
          inactiveOpacity={0.15}
          startLabelTextColor={{ theme: "background" }}
          endLabelTextColor={{ from: "color", modifiers: [] }}
          pointSize={4}
          inactivePointSize={0}
          pointColor={{ from: "serie.color", modifiers: [] }}
          pointBorderWidth={3}
          activePointBorderWidth={3}
          pointBorderColor={{ from: "serie.color" }}
          enableGridX={false}
          enableGridY={false}
          axisTop={false}
          axisBottom={{
            tickSize: 5,
            tickPadding: 5,
            tickRotation: 0,
            legend: "",
            legendPosition: "middle",
            legendOffset: 32,
            truncateTickAt: 0,
          }}
          axisLeft={{
            tickSize: 5,
            tickPadding: 5,
            tickRotation: 0,
            legend: "",
            legendPosition: "middle",
            legendOffset: -40,
            scale: "linear", // Mantenha a escala linear
            format: (value) => Math.abs(value), // Formata a escala para números positivos
          }}
          margin={{ top: 50, right: 130, bottom: 50, left: 60 }}
          axisRight={null}
          theme={{
            tooltip: {
              container: {
                background: "#fff", // cor de fundo do tooltip
                color: "#000", // cor do texto do tooltip
              },
            },
            axis: {
              domain: {
                line: {
                  stroke: colors.grey[100],
                },
              },
              legend: {
                text: {
                  fill: colors.grey[100],
                },
              },
              ticks: {
                line: {
                  stroke: colors.grey[100],
                  strokeWidth: 1,
                },
                text: {
                  fill: colors.grey[100],
                },
              },
            },
            legends: {
              text: {
                fill: colors.grey[100],
              },
            },
          }}
        />
      </>
    );
  }
}
 
  ```
</details>

<details>
  <summary>Filtros na tela do mapa</summary>
	
	Descrição da atividade 
  
  ```javascript
 
  ```
</details>

<details>
  <summary>Filtros na tela dashboard</summary>
	
	Descrição da atividade 
  
  ```javascript
 
  ```
</details>

<details>
  <summary>Conexão filtro sentimento e ajustes</summary>
	
	Descrição da atividade 
  
  ```javascript
 
  ```
</details>

<details>
  <summary>Inclusão do DOCX para baixar relatório</summary>
	
	A função handleDownloadReport cria e baixa um relatório .docx contendo texto formatado. Ela usa a biblioteca docx para construir o documento e file-saver para salvar o arquivo localmente.
  
  ```javascript
  const handleDownloadReport = () => {
    const doc = new Document({
      sections: [{
        properties: {},
        children: [
          new Paragraph({
            children: [
              new TextRun("Ralatório HexAnalytics"),
              new TextRun({
                text: "Foo Bar",
                bold: true,
              }),
              new TextRun({
                text: "\tExemplos",
                bold: true,
              }),
            ],
          }),
        ],
      }]
    });

    Packer.toBlob(doc).then(blob => {
      console.log(blob);
      saveAs(blob, "relatorio.docx");
      console.log("Document created successfully");
    });
  }
 
  ```
</details>

<details>
  <summary>Relatório do dashboard</summary>
	
	A função createDocxContent cria um documento .docx formatado com subtítulos, listas de sentimentos e gráficos/imagens, 
 	usando a biblioteca docx. O conteúdo inclui valores totais, valores das pesquisas e as imagens dos gráficos e da nuvem 
  	de palavras. 
  
  ```javascript

// src/docxContent.js

import { AlignmentType, Document, Paragraph, TextRun, HeadingLevel, ImageRun } from 'docx';

function numberWithCommas (x) {
  return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
}

export const createDocxContent = (feelingAll, feelingData, imageBlobs) => {
  const subtitles = [
    { text: "Total dos dados de vendas das lojas Americanas do ano de 2018.", feeling: feelingAll },
    // { text: "Total dos dados da pesquisa:" },
    // { text: "Selecionado os estados ou região: São Paulo e Acre.", feeling: feelingData },
    { text: "Total definido pelo filtro:", feeling: feelingData },
    { text: "Gráficos demonstrativos" },
    { text: "Gender:", imageBlob: imageBlobs.genderChartBlob, size: [250, 400] },
    { text: "Review sentiment by month:", imageBlob: imageBlobs.sentimentByMonthChartBlob, size: [250, 600] },
    { text: "Reviews by Category:", imageBlob: imageBlobs.reviewsByCategoryBlob, size: [250, 400] },
    { text: "Top Words:", imageBlob: imageBlobs.topWordsBlob, size: [250, 400] }
  ]

  const bullets = [
    {content: "Total de positivo:", key: 'positive'},
    {content: "Total de neutro:", key: 'neutral'},
    {content: "Total de negativo:", key: 'negative'},
  ]

  const breakLine = () => {
    return new Paragraph({
      text: "",
      alignment: AlignmentType.CENTER,
    })
  }

  const getSubtitles = () => {
    const contents = [];

    for (let index = 0; index < subtitles.length; index++) {
      contents.push(breakLine()),
      contents.push(
        new Paragraph({
          children: [
            new TextRun({
              text: subtitles[index],
              bold: true,
              font: "Aptos",
              size: 24,
              color: "92BAF7"
            })
          ],
        })
      )

      if (subtitles[index].feeling) {
        contents.push(breakLine())
        contents.push(...getBullets(subtitles[index].feeling))
        contents.push(breakLine())
      }
      
      if (subtitles[index].imageBlob) {
        contents.push(breakLine())
        contents.push(getImageFromBlob(subtitles[index].imageBlob, subtitles[index].size))
        contents.push(breakLine())
      }
    }

    return contents;
  }

  const getBullets = (myFeeling) => {
    return bullets.map((bulletText, index) => {
      return new Paragraph({
        children: [
          new TextRun({
            text: `${bulletText.content}`,
            bold: true,
            font: "Aptos",
            size: 24
          }),
          new TextRun({
            text: ` ${numberWithCommas(myFeeling[bulletText.key])} mil`,
            font: "Aptos",
            size: 24
          })
        ],
        bullet: { level: 0 }
      })
    }
    )
  }

  const getImageFromBlob = (myBlobData, size) => {
    return new Paragraph({
      children: [
        new ImageRun({
          type: "jpg",
          data: myBlobData,
          transformation: {
            height: size[0],
            width: size[1]
          }
        })
      ]
    })
  }

  return new Document({
    styles: {
      default: {
        heading1: {
          run: {
            size: 32,
            bold: true,
            color: "000000",
            font: "Aptos"
          },
          paragraph: {
            alignment: AlignmentType.CENTER,
            spacing: {
              after: 120,
            },
          },
        },
        heading2: {
          run: {
            size: 74,
            bold: true,
            color: "92BAF7",
            font: "Aptos"
          },
          paragraph: {
            spacing: {
              before: 600,
              after: 120,
            },
          }
        },
      },
    },
    paragraphStyles: [
      {
          id: "subtitle",
          name: "Subtitle",
          basedOn: "Normal",
          next: "Normal",
          run: {
            size: 12,
            bold: true,
            color: "92BAF7",
            font: "Aptos"
          },
          paragraph: {
            spacing: {
              before: 240,
              after: 120,
            },
          }
      }
  ],
    sections: [
      {
        properties: {},
        children: [
          new Paragraph({
            text: "Relatório Dashboard HexAnalytics",
            heading: HeadingLevel.HEADING_1,
          }),
          ...getSubtitles(),
        ],
      },
    ],
  });
};

 
  ```
</details>

<details>
  <summary>Relatório do mapa</summary>

 	A função createDocxContent cria um documento .docx, usando a biblioteca docx. O conteúdo inclui valores totais, 
  	valores das pesquisas, nome das regiões pesquisadas e o mapa do brasil de acordo com os sentimentos, com dados 
   	obtidos de um serviço externo.
  
  ```javascript
// src/docxContent.js

import { AlignmentType, Document, Paragraph, TextRun, HeadingLevel, ImageRun } from 'docx';
import { getFeeling } from '../../services/SalesService';

function numberWithCommas (x) {
  return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
}

export const createDocxContent = async (mapBlob, selectedFeeling, selectedRegion, selectedStates,) => {

  const feelingData = [];
  const feelingDataFiltered = [];
  let data;

  data = await getFeeling()
  data.forEach((row) => {
    feelingData[row._id.toLowerCase()] = row.count.toLocaleString('pt-BR');
    feelingData["total"] += row.count;
  });

  data = await getFeeling(selectedStates, selectedRegion)
  data.forEach((row) => {
    feelingDataFiltered[row._id.toLowerCase()] = row.count.toLocaleString('pt-BR');
    feelingDataFiltered["total"] += row.count;
  });

  const subtitles = [
    // { text: "Total dos dados de vendas das lojas Americanas do ano de 2018.", hasData: true },
    // { text: "Total dos dados da pesquisa:" },
    { text: "Filtros selecionados: ", bulletIndex: 0 },
    { text: "Total dos dados de vendas das lojas Americanas do ano de 2018:", bulletIndex: 1 },
    { text: "Total definido pelo filtro:", bulletIndex: 2 },
    { text: "Filtragem por sentimentos:" },
    { text: "Mapa do Brasil:", imageBlob: mapBlob },
  ]

  const bullets = {
    0: [
      { content: "Sentimento:", value: selectedFeeling.toUpperCase() },
      { content: "Região:", value: selectedRegion.toUpperCase() },
      { content: "Estados:", value: selectedStates.join(', ') }
    ],
    1: [
      { content: "Total de positivo:", value: `${feelingData.positive} mil` },
      { content: "Total de neutro:", value: `${feelingData.neutral} mil` },
      { content: "Total de negativo:", value: `${feelingData.negative} mil` }
    ],
    2: [
      { content: "Total de positivo:", value: `${feelingDataFiltered.positive} mil` },
      { content: "Total de neutro:", value: `${feelingDataFiltered.neutral} mil` },
      { content: "Total de negativo:", value: `${feelingDataFiltered.negative} mil` }
    ]
  };

  const breakLine = () => {
    return new Paragraph({
      text: "",
      alignment: AlignmentType.CENTER,
    })
  }

  const getSubtitles = () => {
    const contents = [];

    for (let index = 0; index < subtitles.length; index++) {
      contents.push(breakLine()),
        contents.push(
          new Paragraph({
            children: [
              new TextRun({
                text: subtitles[index],
                bold: true,
                font: "Aptos",
                size: 24,
                color: "92BAF7"
              })
            ],
          })
        )

      if (subtitles[index].hasOwnProperty('bulletIndex')) {
        contents.push(breakLine())
        contents.push(...getBullets(subtitles[index].bulletIndex))
        contents.push(breakLine())
      }

      if (subtitles[index].imageBlob) {
        contents.push(breakLine())
        contents.push(getImageFromBlob(subtitles[index].imageBlob))
        contents.push(breakLine())
      }
    }

    return contents;
  }

  const getBullets = (bulletIndex) => {
    return bullets[bulletIndex].map(bulletText => {
      return new Paragraph({
        children: [
          new TextRun({
            text: `${bulletText.content}`,
            bold: true,
            font: "Aptos",
            size: 24
          }),
          new TextRun({
            text: ` ${bulletText.value}`,
            font: "Aptos",
            size: 24
          })
        ],
        bullet: { level: 0 }
      })
    })
  }

  const getImageFromBlob = (myBlobData) => {
    return new Paragraph({
      children: [
        new ImageRun({
          type: "jpg",
          data: myBlobData,
          transformation: {
            width: 540,
            height: 400
          }
        })
      ]
    })
  }

  return new Document({
    styles: {
      default: {
        heading1: {
          run: {
            size: 32,
            bold: true,
            color: "000000",
            font: "Aptos"
          },
          paragraph: {
            alignment: AlignmentType.CENTER,
            spacing: {
              after: 120,
            },
          },
        },
        heading2: {
          run: {
            size: 74,
            bold: true,
            color: "92BAF7",
            font: "Aptos"
          },
          paragraph: {
            spacing: {
              before: 600,
              after: 120,
            },
          }
        },
      },
    },
    paragraphStyles: [
      {
        id: "subtitle",
        name: "Subtitle",
        basedOn: "Normal",
        next: "Normal",
        run: {
          size: 12,
          bold: true,
          color: "92BAF7",
          font: "Aptos"
        },
        paragraph: {
          spacing: {
            before: 240,
            after: 120,
          },
        }
      }
    ],
    sections: [
      {
        properties: {},
        children: [
          new Paragraph({
            text: "Relatório Mapa HexAnalytics",
            heading: HeadingLevel.HEADING_1,
          }),
          ...getSubtitles(),
        ],
      },
    ],
  });
};

 
  ```
</details>


<div align="center">

**Hard Skills**
|**Tecnologia/Metodologia**|**Classificação**      |
|--------------------------|-----------------------|
|HTML                      |Sei fazer com Autonomia|
|CSS                       |Sei fazer com Autonomia|
|JavaScript                |Sei fazer com Ajuda    |
|React                     |Sei fazer com Ajuda    |
|MUI                       |Sei fazer com Ajuda    |
|Git                       |Sei fazer com Ajuda    |
|GitHub                    |Sei fazer com Ajuda    |
|Jira Software             |Sei fazer com Ajuda    |
|Python                    |Entendi                |
|Flesk                     |Entendi                |
|Mongodb compass           |Entendi                |


**Soft Skills**
|**Habilidade**     |**Descrição**        |
|-------------------|---------------------|
|Organização|Capacidade de planejar e gerenciar tarefas de forma eficiente.|
|Trabalho em Equipe|Habilidade de colaborar e comunicar efetivamente com outros membros da equipe para alcançar objetivos comuns.|
|Proatividade|Iniciativa para identificar e abordar problemas, capacidade de buscar oportunidades de melhoria sem a necessidade de supervisão.|
|Confiança|Autoconfiança e a capacidade de confiar nos próprios conhecimentos e habilidades, bem como nos outros membros da equipe.|
|Lógica de programação|Capacidade de pensar logicamente e resolver problemas de forma estruturada e eficaz usando algoritmos e técnicas de programação.|

</div>


___________
<div align="justify">

## Outros Projetos:

- [1° Semestre API 1: Ivy - Assistente virtual para auxiliar na produtividade](https://github.com/HelenAlevato/Bertoti/blob/main/Metodologia%20da%20Pesquisa%20Cientifico%20Tecnol%C3%B3gica/API_1.md) 
- [2° Semestre API 2: G6 - Sistema de digitação e edição de contas](https://github.com/HelenAlevato/Bertoti/blob/main/Metodologia%20da%20Pesquisa%20Cientifico%20Tecnol%C3%B3gica/API%20_2.md)
- [3° Semestre API 3: 14 BIS - Software para otimiza a criação e controle de documentos de aeronaves](https://github.com/HelenAlevato/Bertoti/blob/main/Metodologia%20da%20Pesquisa%20Cientifico%20Tecnol%C3%B3gica/API%20_3.md)
- [4° Semestre API 4: LeFoot - Sistema para tomada de decisões na criação de campanhas e compras de produtos ](https://github.com/HelenAlevato/Bertoti/blob/main/Metodologia%20da%20Pesquisa%20Cientifico%20Tecnol%C3%B3gica/API%20_4.md)
- [5° Semestre API 5: Persuance - Desenvolver uma aplicação para utilização da norma, exibindo as palavras aprovadas ou não aprovadas para consulta e verificação de textos](https://github.com/HelenAlevato/Bertoti/blob/main/Metodologia%20da%20Pesquisa%20Cientifico%20Tecnol%C3%B3gica/API_5.md)
- [6° Semestre API 6: HexAnalytics - Desenvolver uma aplicação de análise de sentimento, com bons insights](https://github.com/HelenAlevato/Bertoti/blob/main/Metodologia%20da%20Pesquisa%20Cientifico%20Tecnol%C3%B3gica/API_6.md)

</div>
