<template>
    <div class="header">
        <div class="header__left">
            <span class="material-icons " @click="menuTogg " >menu</span>
            <!-- <p></p> -->
            <a href="#">
                <img src="https://i.pinimg.com/originals/ae/47/fa/ae47fa9a8fd263aa364018517020552d.png" alt="loading image" />
            </a>
        </div>
        <div class="header__middle" >
            <span class="material-icons"> search </span>
            <input type="text" placeholder="Search mail">
            <span class="material-icons"> arrow_drop_down </span>
        </div>

        <div class="header__right">
            <span class="material-icons"> apps </span>
            <span class="material-icons"> notifications </span>
            <span class="material-icons"> account_circle </span>
        </div>
    </div>
</template>

<script>
    export default{

    }
</script>