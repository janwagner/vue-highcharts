<template>
    <div id="app">
        <h1>
            <a href="https://github.com/superman66/vue-highcharts" target="_blank">
                Vue-Highcharts
                <p>the component of Vue 2+ for Highcharts</p>
            </a>
        </h1>
        <section class="chart-list">
            <section class="charts">
                <h3>Line Basic
                    <p>load data with async</p>
                </h3>
                <vue-highcharts :options="options" ref="lineCharts"></vue-highcharts>
                <button @click="remove">remove Series</button>
                <button @click="add">add Series</button>
            </section>
        </section>

    </div>
</template>
<script>
import VueHighcharts from '../src/VueHighcharts.vue'
import Drilldown from '../node_modules/highcharts/modules/drilldown.js'
import * as data from '../data/data'
import Highcharts from 'highcharts'
Drilldown(Highcharts);
export default {
    components: {
        VueHighcharts
    },
    data() {
        return {
            Highcharts: Highcharts,
            options: data.initial,
            areaOptions: data.AreaData,
            pieOptions: data.PieData,
            drilldownOptions: data.DrilldownData
        }
    },
    mounted() {

    },
    methods: {
        load() {
            let lineCharts = this.$refs.lineCharts;
            //charts.showLoading('loading');

            // you also can use the delegateMethod()
            lineCharts.delegateMethod('showLoading', 'Loading...');
            setTimeout(() => {
                lineCharts.addSeries(data.asyncData);
                lineCharts.hideLoading();
            }, 2000)
        },
        update() {
            let lineCharts = this.$refs.lineCharts;
            lineCharts.getChart().xAxis[0].setCategories(['J', 'F', 'M', 'A', 'M', 'J', 'J', 'A', 'S', 'O', 'N', 'D']);
        },
        remove() {
            this.$refs.lineCharts.removeSeries();
        },
        add() {
            this.$refs.lineCharts.addSeries({
                regression: true,
                regressionSettings: {
                    type: 'polynomial',
                    color: 'rgba(223, 83, 83, .9)',
                    extrapolate: 5
                },
                name: 'Test input',
                color: 'rgba(223, 83, 83, .5)',
                data: [
                    /* Dec 2017 */
                    [1512086400000,171.05],
                    [1512345600000,169.80],
                    [1512432000000,169.64],
                    [1512518400000,169.01],
                    [1512604800000,169.32],
                    [1512691200000,169.37],
                    [1512950400000,172.67],
                    [1513036800000,171.70],
                    [1513123200000,172.27],
                    [1513209600000,172.22],
                    [1513296000000,173.97],
                    [1513555200000,176.42],
                    [1513641600000,174.54],
                    [1513728000000,174.35],
                    [1513814400000,175.01],
                    [1513900800000,175.01],
                    [1514246400000,170.57],
                    [1514332800000,170.60],
                    [1514419200000,171.08],
                    [1514505600000,169.23],
                ]
            })
        }
    }
};
</script>
<style lang="scss" rel="stylesheet/scss" type="text/css">
$chartWidth: 600px;
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

html,
body {
    margin: 0;
    padding: 0;
    background: rgba(37, 37, 37, 0.84);
}

#app {}

h1 {
    font-family: Dosis, "Source Sans Pro", "Helvetica Neue", Arial, sans-serif;
    padding: 2em 0 1em;
    text-align: center;
    a {
        text-decoration: none;
        color: #ccc;
    }
}

h1,
h3 {
    color: #ccc;
    font-weight: 300;
    p {
        font-size: 14px;
        margin: 5px;
    }
}

.charts {
    width: $chartWidth;
    margin: 0 auto;
    padding-bottom: 2em;
    text-align: center;
    h3 {
        text-align: center;
        margin: 0;
    }
    button {
        padding: 5px 20px;
        background: #fff;
        -webkit-appearance: none;
        border: 1px solid #c5c5c5;
        border-radius: 5px;
        outline: none;
        &:hover {
            background: lightgray;
            color: #333;
        }
    }
}

.highcharts {
    display: inline-block;
    margin: 2em auto;
    border: 1px solid rgba(0, 0, 0, 0.1);
    border-radius: 8px;
    box-shadow: 0 0 45px rgba(0, 0, 0, 0.2);
    padding: 1.5em 0em;
    background: #fff;
}
</style>
