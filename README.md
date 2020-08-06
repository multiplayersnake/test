function interval(){
    httpGetAsync("https://api.coinbase.com/v2/prices/ETH-USD/spot", (response, request) => {
        let parsed = JSON.parse(response);
        client.guilds.cache.forEach(server => {

            let currentprince = parseFloat(parsed.data.amount);
            let diff = currentprince - previousprice;

            
            
            
            if(diff.toFixed(2)!=0){
                let char = "";
                if(diff > 0){
                    char = "↑";
                }else{
                    char = "↓";
                }
                previousprice = parseFloat(parsed.data.amount);
                let percentage = diff/100;
                percentage = percentage.toFixed(2);
                if(percentage<0){
                    percentage = ""+percentage;
                    percentage = percentage.substr(1);
                }
                server.member(client.user).setNickname(parsed.data.amount+""+char+percentage+"%");
            }
            /*
             server.members.cache.forEach(e=>{
                 if(e.user.id == '740604908880920737'){
                     
                 }
                 
             });
             */
        });
    });
}
