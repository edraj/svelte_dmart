<script>
  import { Bar,Bubble } from 'svelte-chartjs';

  import {
    Chart,
    Title,
    Tooltip,
    Legend,
    BarElement,
    CategoryScale,
    PointElement,
    LinearScale,
  } from 'chart.js';

  Chart.register(
    Title,
    Tooltip,
    Legend,
    BarElement,
    CategoryScale,
    PointElement,
    LinearScale
  );

const dataBar = {
  labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
  datasets: [
    {
      label: '% of Votes',
      data: [12, 19, 3, 5, 2, 3],
      backgroundColor: [
        'rgba(255, 134,159,0.4)',
        'rgba(98,  182, 239,0.4)',
        'rgba(255, 218, 128,0.4)',
        'rgba(113, 205, 205,0.4)',
        'rgba(170, 128, 252,0.4)',
        'rgba(255, 177, 101,0.4)',
      ],
      borderWidth: 2,
      borderColor: [
        'rgba(255, 134, 159, 1)',
        'rgba(98,  182, 239, 1)',
        'rgba(255, 218, 128, 1)',
        'rgba(113, 205, 205, 1)',
        'rgba(170, 128, 252, 1)',
        'rgba(255, 177, 101, 1)',
      ],
    },
  ],
};
const dataBubble = {
  labels: 'Bubble',
  datasets: [
    {
      label: 'John',
      data: [
        {
          x: 3,
          y: 7,
          r: 10,
        },
      ],
      backgroundColor: '#ff6384',
      hoverBackgroundColor: '#ff6384',
    },
    {
      label: 'Peter',
      data: [
        {
          x: 3.2,
          y: 7,
          r: 10,
        },
      ],
      backgroundColor: '#44e4ee',
      hoverBackgroundColor: '#44e4ee',
    },
    {
      label: 'Donald',
      data: [
        {
          x: 3.4,
          y: 7,
          r: 10,
        },
      ],
      backgroundColor: '#62088A',
      hoverBackgroundColor: '#62088A',
    },
  ],
};
</script>

# Charts

Examples of charts.

## Bar

<Bar data={dataBar} options={{ responsive: true }} />

## Bubble

<Bubble data={dataBubble} options={{ responsive: true }} />

## And many more

You can find more examples in the [chart.js documentation](https://www.chartjs.org/docs/latest/), also by using the svelte wrapper [svelte-chartjs](https://www.npmjs.com/package/svelte-chartjs)


