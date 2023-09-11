# Server-Side
Materia de Server Side
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
exe 1:
um conjunto de leitores respondeu a um survey(pesquisa)que continha as seguintes perguntas: qual a idade de cada  leitor?
Em qual  cidade  o leitor mora?
E a opinião em  relação ao livro que  fora  lançado meses atrás,
 em que o leitor respondeuma das seguintes opções: 
3-ótimo,
2 -bom,
1 –regular.
Escreva um programa que receba a idade
a cidade e a opinião de 16 leitores
calcule e exiba: a média das idades dos leitores que responderam ótimo
a quantidade de leitores que responderam regular
a porcentagem de leitores que responderam bom entre todos os leitores
a porcentagem de leitores para cada cidade.

Código:

const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

let idadeTotalOtimo = 0; // Variável para a soma das idades dos leitores que responderam "ótimo"
let quantidadeRegular = 0; // Variável para a soma das idades dos leitores que responderam "regular"
let quantidadeBom = 0; // Variável para a soma das idades dos leitores que responderam "bom"
let quantidadeTotal = 0; // Variável para o número total de leitores
const cidadeOpinioes = {}; // Objeto para armazenar os leitores por cidade

// Função para calcular a porcentagem
function calcularPorcentagem(valor, total) {
  return (valor / total) * 100;
}

// Função para exibir os resultados finais
function exibirResultados() {
  console.log(`Média de idades dos leitores que responderam "ótimo": ${idadeTotalOtimo / quantidadeOtimo}`);
  console.log(`Quantidade de leitores que responderam "regular": ${quantidadeRegular}`);
  console.log(`Porcentagem de leitores que responderam "bom" entre todos os leitores: ${calcularPorcentagem(quantidadeBom, quantidadeTotal)}%`);
  console.log('Porcentagem de leitores por cidade:');
  for (const cidade in cidadeOpinioes) {
    const totalCidade = cidadeOpinioes[cidade].total;
    const bomCidade = cidadeOpinioes[cidade].bom;
    console.log(`${cidade}: ${calcularPorcentagem(bomCidade, totalCidade)}%`);
  }
  rl.close();
}

// Função para fazer perguntas
function fazerPerguntas() {
  rl.question('Qual é a idade do leitor? ', (idade) => {
    rl.question('Em qual cidade o leitor mora? ', (cidade) => {
      rl.question('Qual é a opinião do leitor (1-regular, 2-bom, 3-ótimo)? ', (opiniao) => {
        idade = parseInt(idade); // Converte a idade de string para número
        quantidadeTotal++; // Incrementa o número total de leitores
        if (opiniao === '3') {
          idadeTotalOtimo += idade; // Soma a idade do leitor que respondeu "ótimo"
          quantidadeOtimo++; // Incrementa a quantidade de leitores que responderam "ótimo"
        } else if (opiniao === '1') {
          quantidadeRegular++; // Incrementa a quantidade de leitores que responderam "regular"
        } else if (opiniao === '2') {
          quantidadeBom++; // Incrementa a quantidade de leitores que responderam "bom"
        }
        if (cidadeOpinioes[cidade]) {
          cidadeOpinioes[cidade].total++; // Incrementa a contagem de leitores para a cidade
          if (opiniao === '2') {
            cidadeOpinioes[cidade].bom++; // Incrementa a contagem de leitores que responderam "bom" para a cidade
          }
        } else {
          cidadeOpinioes[cidade] = {
            total: 1, // Inicializa a contagem de leitores para a cidade
            bom: opiniao === '2' ? 1 : 0 // Inicializa a contagem de leitores que responderam "bom" para a cidade
          };
        }
        if (quantidadeTotal < 16) {
          fazerPerguntas(); // Continue fazendo perguntas até atingir 16 leitores
        } else {
          exibirResultados(); // Exiba os resultados finais quando todas as perguntas forem respondidas
        }
      });
    });
  });
}

// Inicia o processo de fazer perguntas para os leitores
fazerPerguntas();
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
exe 2:
Em  uma  certificação  são  feitos  5  exames  (I,  II,  III,  IV  e  V). Escreva  um  programa  que  leia as  notas  desses
exames e imprima a classificação do interessado na certificação, sabendo que a média é 70. Classificação:
A –passou em todos os exames
B –passou em I, II e IV, mas não em III ou V
C –passou em I e II, III ou IV, mas não em V.
Reprovado outras situações.

Código:

const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

// Função para calcular a classificação com base nas notas dos exames
function calcularClassificacao(notas) {
  const media = (notas.I + notas.II + notas.III + notas.IV + notas.V) / 5;

  if (media >= 70) {
    if (notas.I >= 70 && notas.II >= 70 && notas.IV >= 70) {
      return 'A - passou em todos os exames';
    } else if (notas.I >= 70 && notas.II >= 70 && (notas.III < 70 || notas.V < 70)) {
      return 'B - passou em I, II e IV, mas não em III ou V';
    } else if ((notas.I >= 70 && notas.II >= 70) || (notas.I >= 70 && notas.IV >= 70)) {
      return 'C - passou em I e II, III ou IV, mas não em V';
    } else {
      return 'Reprovado';
    }
  } else {
    return 'Reprovado';
  }
}

// Função principal para receber notas e calcular a classificação
function receberNotas() {
  rl.question('Digite a nota do Exame I: ', (notaI) => {
    rl.question('Digite a nota do Exame II: ', (notaII) => {
      rl.question('Digite a nota do Exame III: ', (notaIII) => {
        rl.question('Digite a nota do Exame IV: ', (notaIV) => {
          rl.question('Digite a nota do Exame V: ', (notaV) => {
            const notas = {
              I: parseFloat(notaI),
              II: parseFloat(notaII),
              III: parseFloat(notaIII),
              IV: parseFloat(notaIV),
              V: parseFloat(notaV)
            };

            const classificacao = calcularClassificacao(notas);
            console.log(`Classificação: ${classificacao}`);
            rl.close();
          });
        });
      });
    });
  });
}

// Inicia o processo de receber notas e calcular a classificação
receberNotas();
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
exe 3:
Chama-se ano bissexto o ano ao qual é acrescentado um dia extra, ficando ele com 366 dias
um dia a mais do que os anos normais de 365 dias, ocorrendo a cada quatro anos
Escreva um programa que verifique se um ano é  bissexto
Um  ano  é  bissexto  se  ele  é  divisível  por  4
Entretanto,  se  o  ano  é  divisível  por  100,  ele  não  é bissexto
Mas, se ele for divisível por 400, ele volta a ser bissexto.
a.São bissextos os anos: 1600, 1996, 2000, 2004, 2008, 2012, 2016, 2400, 2800, ...
b.Não são bissextos: 1500, 1974, 1982, 1983, 1990, 2018, 2022, 2030, 2038, ...

Código: 

const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

// Função para verificar se um ano é bissexto
function verificarAnoBissexto(ano) {
  // Verifica se o ano é divisível por 4 e não é divisível por 100 OU é divisível por 400
  if ((ano % 4 === 0 && ano % 100 !== 0) || ano % 400 === 0) {
    return true; // Se atender às condições, é um ano bissexto
  } else {
    return false; // Caso contrário, não é um ano bissexto
  }
}

rl.question('Digite um ano para verificar se é bissexto: ', (ano) => {
  ano = parseInt(ano); // Converte a entrada do usuário para um número inteiro

  const isBissexto = verificarAnoBissexto(ano); // Chama a função para verificar se o ano é bissexto

  if (isBissexto) {
    console.log(`${ano} é um ano bissexto.`);
  } else {
    console.log(`${ano} não é um ano bissexto.`);
  }

  rl.close(); // Fecha a interface de leitura
});
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
exe 4:
O Hipermercado Tabajara está com uma promoção de carnes que é imperdível. Confira:
                       Até 5 Kg           Acima de 5 Kg
File Duplo          R$ 24,90 por Kg      R$ 25,80 por Kg
Alcatra             R$ 25,90 por Kg      R$ 26,80 por Kg
Picanha             R$ 36,90 por Kg      R$ 37,80 por Kg
Para  atender  os  clientes,  cada  cliente  poderá  levar  apenas  um  dos  tipos  de  carne  da  promoção,
porém  não  há limites para a quantidade de carne por cliente.
Se  compra  for  feita  no  cartão  Tabajara  o  cliente  receberá  ainda  um  desconto  de  5%  sobre  o  total  da  compra.
Escreva um programa que peça o tipo e a quantidade de carne comprada pelo usuário e gere um cupom fiscal, contendo  as  informações  da  compra:
tipo  e  quantidade  de  carne,  preço  total,  tipo  de  pagamento,  valor  do desconto e valor a pagar.

Código:

const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

// Preços da carne por Kg
const precos = {
  'File Duplo': {
    ate5Kg: 24.90,
    acima5Kg: 25.80
  },
  'Alcatra': {
    ate5Kg: 25.90,
    acima5Kg: 26.80
  },
  'Picanha': {
    ate5Kg: 36.90,
    acima5Kg: 37.80
  }
};

// Função para calcular o valor total da compra
function calcularValorTotal(tipoCarne, quantidadeKg) {
  if (quantidadeKg <= 5) {
    return quantidadeKg * precos[tipoCarne].ate5Kg;
  } else {
    return quantidadeKg * precos[tipoCarne].acima5Kg;
  }
}

// Pergunta ao usuário o tipo de carne
rl.question('Digite o tipo de carne (File Duplo, Alcatra ou Picanha): ', (tipoCarne) => {
  // Pergunta ao usuário a quantidade em Kg
  rl.question('Digite a quantidade em Kg: ', (quantidadeKg) => {
    // Pergunta ao usuário se a compra será feita com o cartão Tabajara
    rl.question('A compra será feita com o cartão Tabajara? (S para sim, N para não): ', (cartaoTabajara) => {
      quantidadeKg = parseFloat(quantidadeKg); // Converte a quantidade para número decimal

      // Verifica se a quantidade é válida
      if (isNaN(quantidadeKg) || quantidadeKg <= 0) {
        console.log('Quantidade inválida. Por favor, digite um valor válido.');
        rl.close();
        return;
      }

      // Calcula o valor total da compra
      const valorTotal = calcularValorTotal(tipoCarne, quantidadeKg);

      // Calcula o desconto (se aplicável)
      const desconto = cartaoTabajara === 'S' ? valorTotal * 0.05 : 0;

      // Calcula o valor a pagar
      const valorAPagar = valorTotal - desconto;

      // Exibe o cupom fiscal
      console.log('\nCupom Fiscal:');
      console.log(`Tipo de carne: ${tipoCarne}`);
      console.log(`Quantidade: ${quantidadeKg} Kg`);
      console.log(`Preço total: R$ ${valorTotal.toFixed(2)}`);
      console.log(`Tipo de pagamento: ${cartaoTabajara === 'S' ? 'Cartão Tabajara' : 'Dinheiro'}`);
      console.log(`Valor do desconto: R$ ${desconto.toFixed(2)}`);
      console.log(`Valor a pagar: R$ ${valorAPagar.toFixed(2)}`);

      rl.close(); // Fecha a interface de leitura
    });
  });
});
