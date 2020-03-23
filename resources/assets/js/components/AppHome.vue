<template>
    <div>
        <v-container>
            <toolbar></toolbar>
            <router-view></router-view>
            <app-footer></app-footer>
        </v-container>
        
    </div>
</template>

<script>
import toolbar from './Toolbar'
import AppFooter from './AppFooter'
import Login from './login/Login'

export default {
    components:{toolbar,AppFooter,Login}    
}
</script>

<style>
    
</style>