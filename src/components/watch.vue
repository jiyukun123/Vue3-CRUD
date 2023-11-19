<template>
  <div class="table-box">
    <div class="title">
      <h2>CRUD-DEMO</h2>
    </div>
    <div class="query-box">
      <el-input @input="handleQueryName" v-model="queryInput" placeholder="请输入">你好</el-input>
      <div>
        <el-button type="primary" @click="handleAdd">增加</el-button>
      <el-button type="danger" @click="handleDelete">删除多选</el-button>
      </div>
    </div>
    <div>
      
  <el-table 
    ref="multipleTableRef"
    :data="tableData"
    style="width: 100%"
    @selection-change="handleSelectionChange"
  
  >  <el-table-column type="selection" width="55" />
    
    <el-table-column prop="name" label="名称" width="120" />
    <el-table-column prop="email" label="邮箱" width="120" />
    <el-table-column prop="state" label="状态" width="200" />
    <el-table-column prop="phone" label="号码" width="220" />
    <el-table-column prop="address" label="地址" width="600" /> 
    <el-table-column fixed="right" label="操作" width="120" >
    
      <template #default="scope">
        <el-button 
        link type="primary" 
        size="small" 
        @click.prevent="deleteRow(scope.$index)">
        删除
      </el-button>
        <el-button link type="primary" size="small" @click="handleEdit(scope.row)">编辑</el-button>
      </template>
    </el-table-column>
  </el-table>
 

  <el-dialog v-model="dialogFormVisible" :title="dialogType">
    <el-form :model="tableForm">
      <el-form-item label="请输入姓名" :label-width="100">
        <el-input v-model="tableForm.name" autocomplete="off" />
      </el-form-item>
      <el-form-item label="请输入邮箱" :label-width="100">
        <el-input v-model="tableForm.email" autocomplete="off" />
      </el-form-item>
      <el-form-item label="请输入电话" :label-width="100">
        <el-input v-model="tableForm.phone" autocomplete="off" />
      </el-form-item>
      <el-form-item label="请输入状态" :label-width="100">
        <el-input v-model="tableForm.state" autocomplete="off" />
      </el-form-item>
      <el-form-item label="请输入地址" :label-width="100">
        <el-input v-model="tableForm.address" autocomplete="off" />
      </el-form-item>
    </el-form>
    <template #footer>
      <span class="dialog-footer">
        <el-button type="primary" @click="dialogConfirm ">
        确认
        </el-button>
       
      </span>
    </template>
  </el-dialog>



    </div>
  </div>
</template>

<script setup>
    import { ref } from 'vue';

    let dialogType=ref('add')

      let queryInput = ref()

      const tableData = ref([{
        id:1,
        name: 'Tom',
        email: 'California',
        state: 'Los Angeles',
        phone: '153312312',
        address: '13213123CA 90036',
      },
      {
        id:2,
        name: 'Tom',
        email: 'California',
        state: 'Los Angeles',
        phone: '153312312',
        address: '13213123CA 90036',
      },
      {
        id:3,
        name: 'Tom',
        email: 'California',
        state: 'Los Angeles',
        phone: '153312312',
        address: '13213123CA 90036',
      }
      
       
       
      ])

      const dialogFormVisible = ref(false)

      const multipleSelection = ref([])



      let tableForm=ref({
        name:'小可',
        email:'163@qq123',
        state:'良好',
        phone:'153123123',
        address:'广西省河南'
      })

      const handleSelectionChange = (val) => {
        // multipleSelection.value = val
        multipleSelection.value=[]
        val.forEach(item => {
          multipleSelection.value.push(item.id)
        });
        console.log(multipleSelection.value);
       
       
      }
     
      const handleAdd=()=>{
        dialogFormVisible.value=true
        dialogType.value='add'
        tableForm.value={}
      }


     

      const dialogConfirm=()=>{
        dialogFormVisible.value=false
        if(dialogType.value==='add'){
         
        tableData.value.push({
          id:tableData.value.length+1,
        ... tableForm.value
        })

        }else{
          let index=tableData.value.findIndex(item=>item.id===tableForm.value.id)
        console.log(index);
        tableData.value[index]=tableForm.value



        }
       
        console.log(tableData);
        
       
      }


      const deleteRow = (index) => {

      tableData.value.splice(index, 1)
      console.log(index);
}
      const handleDelete=()=>{
           multipleSelection.value.forEach(id=>{
            deleteRow({id})
           })
      }

      const handleEdit=(row)=>{
        dialogType.value='edit'
        dialogFormVisible.value=true
        tableForm.value={...row}
      }

     let tableDataCopy= Object.assign(tableData.value)
       
    const handleQueryName=(val)=>{
      if(val.length>0){
        tableData.value=tableData.value.filter(item=>(item.name).toLowerCase().match(val.toLowerCase()))
      }else{
        tableData.value=tableDataCopy
      }
    }
        
 
  </script>
<style scoped>
.table-box{
 
  width: 800px;
  margin: 200px auto;
}
.title{
  text-align: center;
}
.query-box{
  display: flex;
  justify-content: space-between;
  margin-bottom: 50px;
}
  .query-box .el-input{
     width: 400px;
  } 
</style>

   



