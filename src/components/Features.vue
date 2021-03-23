<template>
    <div class="main">
      <div class="container">
        <div class="row text-left">
            <div class="col-md-4 col-12 bg-white">
                <div class="list-item">
                  <p><i class="fa fa-id-card"></i>ID do Frete CargoX</p>
                  <p class="itens">{{ info.id }}</p>
                </div>
                <div class="list-item">
                  <p><i class="fa fa-id-card"></i>Nº de pedido do cliente</p>
                  <p class="itens">{{ info.customer_tracking_number }}</p>
                </div>
                <div class="list-item">
                  <p><i class="fa fa-id-card"></i>Motorista</p>
                  <p class="itens trucker">{{ info.trucker.name }}</p>
                </div>
                <div class="list-item">
                  <p><i class="fa fa-id-card"></i>Telefone</p>
                  <p class="itens trucker">{{ info.trucker.phone }}</p>
                </div>
                <div class="list-item">
                  <p><i class="fa fa-id-card"></i>Aplicativo</p>
                  <ul>
                      <li class="itens">Acesso {{ info.trucker.last_app_open_at }}</li>
                      <li class="itens">GPS atualizado {{ info.trucker.last_app_position_at }}</li>
                      <li class="itens">Primeiro acesso {{ info.trucker.first_login_at }}</li>
                      <li class="itens">Versão {{ info.trucker.app_version }}</li>
                  </ul>
                </div>
                <div class="list-item">
                  <p><i class="fa fa-id-card"></i>Veículo</p>
                  <p class="itens">{{ trucks }}</p>
                </div>
                <div class="list-item">
                  <p><i class="fa fa-id-card"></i>Origem</p>
                  <p class="itens">
                      {{ info.origin.address }}, {{info.origin.number}} - {{info.origin.city}} - 
                      {{info.origin.state}} - {{info.origin.zip_code }}
                  </p>
                </div>
                <div class="list-item">
                  <p><i class="fa fa-id-card"></i>Destino</p>
                  <p class="itens">
                      {{ info.destination.address }}, {{info.destination.number}} - {{info.destination.city}} - 
                      {{info.destination.state}} - {{info.destination.zip_code }}
                  </p>
                </div>
                <div class="list-item">
                  <p><i class="fa fa-id-card"></i>Operador</p>
                  <p class="itens trucker">{{ info.trucker_seeker.name }}</p>
                </div>
                <div class="list-item">
                  <p><i class="fa fa-id-card"></i>Venda</p>
                  <p class="itens trucker">{{ info.salesperson.name }}</p>
                </div>
            </div>
            <div class="col-md-4 col-12 bg-white">
              <div class="list-item">
                  <p><i class="fa fa-calendar"></i>Coleta agendada</p>
                  <p class="itens">{{ info.pickup_date }}</p>
                </div>
                <div class="list-item">
                  <p><i></i>Entrega agendada</p>
                  <p class="itens">{{ info.delivery_date }}</p>
                </div>
                <div class="list-item">
                  <p><i></i>Entrega calculada</p>
                  <p class="itens">{{ info.estimated_time_of_arrival }}</p>
                </div>
                <div class="list-item">
                  <p><i></i>Entrega manual</p>
                  <p class="itens">{{ info.manual_input_estimated_time_of_arrival }}</p>
                </div>
                <div class="list-item">
                  <p><i class="fa fa-id-card"></i>Documentos</p>
                  <div class="etiquetas">
                  <span class="badge bg-success">CTe</span>
                  <span class="badge bg-success">MDFe</span>
                  <span class="badge bg-success">Contrato</span>
                  <span class="badge bg-secondary">CIOT</span>
                  </div>
                </div>
                <div class="list-item">
                  <p><i class="fa fa-id-card"></i>Pagamentos</p>
                  <div class="etiquetas">
                  <span class="badge bg-secondary">Adiantamento</span>
                  <span class="badge bg-secondary">Canhoto</span>
                  <span class="badge bg-secondary">Saldo</span>
                  </div>
                </div>
                <div class="list-item">
                  <div class="status">
                    <h4><i class="fa fa-id-card"></i>Status</h4>
                    <ul class="timeline">
                        <li>
                            <p>Agendado</p>
                            <p></p>
                        </li>
                        <li>
                            <p>Indo coletar</p>
                            <p></p>
                        </li>
                        <li>
                            <p>Fila de coleta</p>
                        </li>
                        <li>
                            <p>Carregando</p>
                        </li>
                        <li>
                            <p>Em trânsito</p>
                        </li>
                        <li>
                            <p>Fila descarga</p>
                        </li>
                        <li>
                            <p>Descarregando</p>
                        </li>
                        <li>
                            <p>Entregue</p>
                        </li>
                    </ul>
                  </div>
                </div>
            </div>
            <div class="col-md-4 col-12">
              <GmapMap
                :center="{lat:10, lng:10}"
                :zoom="7"
                map-type-id="terrain"
                style="width: 300px; height: 250px"
                >
                <GmapMarker
                    :key="index"
                    v-for="(m, index) in markers"
                    :position="m.position"
                    :clickable="true"
                    :draggable="true"
                    @click="center=m.position"
                />
                </GmapMap>
            </div>
          </div>
        </div>
      </div>
</template>

<script>
import api from "@/services/api.js";
export default {
    name: "Features",
    data() {
        return {
            info:[],
            trucks:[]
        }
    },
    mounted() {
        api.get("https://www.mocky.io/v2/5c7552e43100009c20c23450").then(response =>{
            this.info = response.data;
        });
        api.get("https://www.mocky.io/v2/5c7552e43100009c20c23450").then(response =>{
            this.trucks = response.data.trucks;
        });
    }
}


</script>

<style scoped>
.list-item:first-child { 
    padding-top: 20px;
    }
    .list-item { 
    padding: 5px 5px;
    }

    .list-item p { 
    vertical-align: middle;
    }

    .list-item i{ 
    margin: 5px 10px;
    }

    .itens {
    padding-left: 40px;
    }

    .trucker{
        text-transform: uppercase;
    }

    .etiquetas {
        color:#fff;
    }
    .etiquetas span {
        margin-right: 3px;
    }

    ul.timeline {
    list-style-type: none;
    position: relative;
}
ul.timeline:before {
    content: ' ';
    background: #d4d9df;
    display: inline-block;
    position: absolute;
    left: 29px;
    width: 2px;
    height: 100%;
    z-index: 400;
}
ul.timeline > li {
    margin: 20px 0;
    padding-left: 20px;
}
ul.timeline > li:before {
    content: ' ';
    background: white;
    display: inline-block;
    position: absolute;
    border-radius: 50%;
    border: 3px solid #22c0e8;
    left: 20px;
    width: 20px;
    height: 20px;
    z-index: 400;
}

</style>