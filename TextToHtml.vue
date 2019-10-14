<template>
    <div class="card">
        <div class="card-header">
            Simple Text to HTML
        </div>

        <div class="card-body">
            <p class="mx-3">
                ** for strong <br>
                **/ for /strong <br>
                __ for em <br>
                __ for /em <br>
                # for headings <br>
            </p>
            <div class="form-group mx-3">
                <label for="text">Text Area</label>
                <textarea name="text" class="form-control mb-2" rows="5" v-model="textValue"></textarea>
                <label for="html">Html Area</label>
                <textarea name="html" class="form-control mb-2" rows="8" v-model="htmlValue"></textarea>

            </div>
            <p class="mx-3">Result</p>
            <div class="m-3 px-3 py-5 border" v-html="htmlValue"></div>
        </div>
    </div>
</template>

<script>
    export default {
        data: function(){
            return {
                textValue : '#this is a heading \n this is a normal paragraph with ** bold **/ and __ emphasize __/ tags. \n####this is a smaller heading'
            }
        },
        computed:{
            htmlValue: function(){
                if(this.textValue){
                    var textArray = this.textValue.split("\n");
                    var HtmlResult = '';
                    for (let i = 0; i < textArray.length; i++) {
                        const line = textArray[i];
                        if(line.startsWith("#####")){
                            HtmlResult += '<h5>' + line.split("#####")[1] + '</h5>\n';
                        }else if(line.startsWith("####")){
                            HtmlResult += '<h4>' + line.split("####")[1] + '</h4>\n';
                        }else if(line.startsWith("###")){
                            HtmlResult += '<h3>' + line.split("###")[1] + '</h3>\n';
                        }else if(line.startsWith("##")){
                            HtmlResult += '<h2>' + line.split("##")[1] + '</h2>\n';
                        }else if(line.startsWith("#")){
                            HtmlResult += '<h1>' + line.split("#")[1] + '</h1>\n';
                        }else{
                            while(line.indexOf("**/")!=-1){
                                line = line.replace("**","<strong>");
                                line = line.replace("**/","</strong>");
                            }
                            while(line.indexOf("__/")!=-1){
                                line = line.replace("__","<em>");
                                line = line.replace("__/","</em>");
                            }
                            
                            HtmlResult += '<p>\n' 
                            HtmlResult += line;
                            HtmlResult += '\n</p>\n';
                        }
                    }
                    return HtmlResult;
                    // return '<h5>' + this.textValue + '</h5>';
                }else{
                    return '';
                }
            }
        },
        methods:{
        }
    }
</script>
