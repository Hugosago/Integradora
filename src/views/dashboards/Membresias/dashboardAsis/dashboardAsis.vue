<script setup lang="ts">
import { computed } from 'vue';
import { ref } from 'vue';
import { useTheme } from 'vuetify';


// common components
import BaseBreadcrumb from '@/components/shared/BaseBreadcrumb.vue';
import UiParentCard from '@/components/shared/UiParentCard.vue';
import UiChildCard from '@/components/shared/UiChildCard.vue';
import { getPrimary, getSecondary } from '@/utils/UpdateColors';
// theme breadcrumb
const page1 = ref({ title: 'Line Chart' });
const breadcrumbs1 = ref([
    {
        text: 'Dashboard',
        disabled: false,
        href: '#'
    },
    {
        text: 'Line Chart',
        disabled: true,
        href: '#'
    }
]);
const chartOptions = computed(() => {
    return {
        chart: {
            height: 350,
            type: 'line',
            fontFamily: `inherit`,
            foreColor: '#adb0bb',
            zoom: {
                type: 'x',
                enabled: true
            },
            toolbar: {
                show: false
            },
            shadow: {
                enabled: true,
                color: '#ff0000',
                top: 18,
                left: 7,
                blur: 10,
                opacity: 1
            }
        },
        colors: [getPrimary.value, getSecondary.value],
        markers: {
            size: 1
        },
        xaxis: {
            categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul'],
            title: {
                text: 'Mes'
            }
        },
        grid: {
            show: false
        },
        dataLabels: {
            enabled: true
        },
        stroke: {
            curve: 'straight',
            width: '2'
        },
        legend: {
            position: 'top',
            horizontalAlign: 'right',
            floating: true,
            offsetY: -25,
            offsetX: -5
        },
        tooltip: {
            theme: 'dark',
            x: {
                format: 'dd/MM/yy HH:mm'
            }
        }
    };
});
const lineChart = {
    series: [
        {
            name: 'Asistencia',
            data: [28, 29, 33, 36, 32, 32, 33]
        },
        {
            name: '',
            data: [12, 11, 14, 18, 17, 13, 13]
        }
    ]
};
const page = ref({ title: 'Column Chart' });
const breadcrumbs = ref([
    {
        text: 'Dashboard',
        disabled: false,
        href: '#'
    },
    {
        text: 'Column Chart',
        disabled: true,
        href: '#'
    }
]);

const theme = useTheme();
const chartOptions1 = computed(() => {
    return {
        chart: {
            type: 'bar',
            height: 350,
            fontFamily: `inherit`,
            foreColor: '#ff0000',
            toolbar: {
              show: false,
            },
        },
        colors: ['#ff0000', '#ff0000', '#f64e60'],
        plotOptions: {
            bar: {
                horizontal: false,
                endingShape: 'rounded',
                columnWidth: '20%'
            }
        },
        dataLabels: {
            enabled: false,
        },
        stroke: {
            show: true,
            width: 2,
            colors: ['transparent']
        },

        xaxis: {
            categories: ['Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct']
        },
        yaxis: {
          title: {
            text: '$ (thousands)',
          },
        },
        fill: {
            opacity: 1
        },
       
        tooltip: {
            theme: 'dark',
            y: {
              formatter(val:any) {
                return `$ ${val} thousands`;
              },
            },
        },
        grid: {
          show: false,
        },
        legend: {
          show: true,
          position: 'bottom',
          width: '50px',
        },
        responsive: [
            {
                breakpoint: 600,
                options: {
                    yaxis: {
                        show: false
                    }
                }
            }
        ]
    };
});

const columnChart = {
    series: [
        {
            name: 'Desktop',
            data: [44, 55, 57, 56, 61, 58, 63, 60, 66]
        },
        {
            name: 'Mobile',
            data: [76, 85, 101, 98, 87, 105, 91, 114, 94]
        },
        {
            name: 'Other',
            data: [35, 41, 36, 26, 45, 48, 52, 53, 41]
        }
    ]
};
</script>


<template>
    <!-- ---------------------------------------------------- -->
    <!-- Line Chart -->
    <!-- ---------------------------------------------------- -->
    <BaseBreadcrumb :title="page1.title" :breadcrumbs1="breadcrumbs1"></BaseBreadcrumb>
    <v-row>
        <v-col cols="12">
            <UiParentCard title="Dashboard 1">
                <apexchart type="line" height="350" :options="chartOptions1" :series="lineChart.series"> </apexchart>
            </UiParentCard>
        </v-col>
    </v-row>

    <!-- ---------------------------------------------------- -->
    <!-- Column Chart -->
    <!-- ---------------------------------------------------- -->
    <BaseBreadcrumb :title="page.title" :breadcrumbs="breadcrumbs"></BaseBreadcrumb>
    <v-row>
        <v-col cols="12">
            <UiParentCard title="Dashboard 1">
                <apexchart type="bar" height="300" :options="chartOptions" :series="columnChart.series"> </apexchart>
            </UiParentCard>
        </v-col>
    </v-row>
</template>
