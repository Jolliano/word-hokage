<style>
    .loader{
        position: relative;
        padding: 40px;
        width: 100%;
        height: 100%;
        z-index: 2;
    }

    .loader:before{
        content: "";
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width:50px;
        height:50px;
        border: 1px solid #ccc;
        border-left: 2px solid transparent;
        border-radius: 50%;
    }
</style>
