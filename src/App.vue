<template>
<div>
    <br>
    <br>
    <div>
        <hr/>
        <br>
        <h2>Cases</h2>
        <CasesLine
        :label="labels"
        :chart-data="confirmed" 
        ></CasesLine>
        <br>
        <br>
        <CasesBar
        :label="labels"
        :chart-data="confirmed" 
        ></CasesBar>
        <br>
        <br>
    </div>
</div>
</template>

<script>
const axios=require("axios")
import CasesBar from '@/components/CasesBar'
import CasesLine from '@/components/CasesLine'
export default {
     data : ()=> {
        return {
            labels : [],
            confirmed : [],
        }

    },
    components : {
        CasesLine,
        CasesBar
    },
    async created() {
  const { data } = await axios.get("https://covid19.mathdro.id/api/confirmed");
  var c=0
  for(var i=0;i<1000;i++){
    if(data[i].countryRegion=="Kenya"){
            if (data[i].provinceState in this.labels){
              continue
            }
            else{
              this.labels.push(data[i].provinceState)
              this.confirmed.push(data[i].confirmed)
              c=c+1
              if(c==28){
                break
              }
            }
          }
  }
console.log(this.labels)
}  
}
</script>