<template>
    <scroller class="wrapper" show-scrollbar="false">
        <div style="height: 40px;"></div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">RSA Hex</text>
        </div>
        <div class="pannel">
            <text class="content">{{hexBuf}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">RSA Base64</text>
        </div>
        <div class="pannel">
            <text class="content">{{base64Buf}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">RSA UrlSafeBase64</text>
        </div>
        <div class="pannel">
            <text class="content">{{urlSafeBase64Buf}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">RSA Verify</text>
        </div>
        <div class="pannel">
            <text class="content">{{verifyBuf}}</text>
        </div>
        <div style="height: 40px;"></div>
    </scroller>
</template>

<script>
    const crypto = weex.requireModule("crypto");
    module.exports = {
        data: {
            verifyBuf: 'SDK版本太低，不支持',
            hexBuf: 'SDK版本太低，不支持',
            base64Buf: 'SDK版本太低，不支持',
            urlSafeBase64Buf: 'SDK版本太低，不支持',
            resultTypes: ['hex', 'base64', 'urlSafeBase64']
        },
        created() {
            if(parseInt(WXEnvironment.weexVersionCode) < 2802) {
                // SDK版本太低
                return;
            }
            for(let idx in this.resultTypes) {
                this.runAlg(this.resultTypes[idx]);
            }
        },
        methods: {
            runAlg(resultType, outBuf) {
                let pemKey = "-----BEGIN RSA PRIVATE KEY-----\n" +
                    "MIICXQIBAAKBgQC1d8wAeHL1FaSOi7DVCOGmvTHDcjpZHnqv8GbWB5g1S0LJnymN\n" +
                    "xuLIhTWzszOxiAqGET4rw3sltai7lcAGaBB2PZpY0CU+P8ppmC+8uTlAI0TdPLhm\n" +
                    "+WqGyyUu3VwwJR48/WhK/0bsUOyjwZi3CQe80TRfnG/EcgehH4GxLbqz5wIDAQAB\n" +
                    "AoGBAKcf9lR0mcLXtN7HDguVC2Spl5wdplkPNgS1DbCN/AMRFihkGjwFcDUmYafn\n" +
                    "IXOeC7sfRDe/57l6DTT9nIUJ8CW3iyTWaYJJel0VNO0RQikYUyIQtBhttaisiszp\n" +
                    "aAQpAYZEavre570nKUCHbnnrmaC93PFbfwdKinQ5BdMmD+UZAkEA5gnNvrN2VCE7\n" +
                    "uMKEuLNQ2xQT7E+cgjp3eOjuzZGD0VVXme4lnNSc1QIgOAcU9MuNzoWzXeUhDLPv\n" +
                    "dZnNu/uBfQJBAMnytrkLCJgL+ggVvx/vKtV3p6AHXnEA3A3g4jgbVqimDBvdIIdS\n" +
                    "u5gjByeP58YeTAyp6tD2awvGQqEn0Z0kCDMCQA+tB1pBfITLJvi2OLklbxMe0SS/\n" +
                    "YBj3xwB0TyGvEt6HBEs3EVUYn/9b/7oRsXnlDSrPraNuY8wrztuiuYRf5TkCQQCd\n" +
                    "oxVYyjESJr8sknUXY2TnLritJTNmOEqNls5fB5AUo1DuayTaHQ2MS0NpcV51eu7Y\n" +
                    "L8a5CLE0hrU6ANARvq+bAkAYXxf1CpMKjJAoT5Sx0jvCcQKZlS2fmoMfJjv/qy0h\n" +
                    "kmZro0KkK1TAB3QWUk3TPOe44YLk1/F13XWYeRIeg5g+\n" +
                    "-----END RSA PRIVATE KEY-----";
                
                let data = "B577CC007872F515A48E8BB0D508E1A6BD31C3723A591E7AAFF066D60798354B42C99F29" +
                    "8DC6E2C88535B3B333B1880A86113E2BC37B25B5A8BB95C0066810763D9A58D0253E3FCA69982FBCB93940" +
                    "2344DD3CB866F96A86CB252EDD5C30251E3CFD684AFF46EC50ECA3C198B70907BCD1345F9C6FC47207A11F" +
                    "81B12DBAB3E7010001";

                crypto.rsaSignOrVerify({
                    algorithm: 'MD5WithRSA',
                    pemkey: pemKey,
                    forSigning: true,
                    data: data,
                    contentType: 'hex',
                    resultType: resultType
                }, (e) => {
                    if(resultType == 'hex') {
                        this.runVerify(e.data);
                    }
                    this[resultType + "Buf"] = e.data;
                });
            },
            runVerify(ciphers) {
                let pemKey = "-----BEGIN RSA PUBLIC KEY-----\n" +
                    "MIGJAoGBALV3zAB4cvUVpI6LsNUI4aa9McNyOlkeeq/wZtYHmDVLQsmfKY3G4siF\n" +
                    "NbOzM7GICoYRPivDeyW1qLuVwAZoEHY9mljQJT4/ymmYL7y5OUAjRN08uGb5aobL\n" +
                    "JS7dXDAlHjz9aEr/RuxQ7KPBmLcJB7zRNF+cb8RyB6EfgbEturPnAgMBAAE=\n" +
                    "-----END RSA PUBLIC KEY-----";

                let data = "B577CC007872F515A48E8BB0D508E1A6BD31C3723A591E7AAFF066D60798354B42C99F29" +
                    "8DC6E2C88535B3B333B1880A86113E2BC37B25B5A8BB95C0066810763D9A58D0253E3FCA69982FBCB93940" +
                    "2344DD3CB866F96A86CB252EDD5C30251E3CFD684AFF46EC50ECA3C198B70907BCD1345F9C6FC47207A11F" +
                    "81B12DBAB3E7010001";
                    
                crypto.rsaSignOrVerify({
                    algorithm: 'MD5WithRSA',
                    pemkey: pemKey,
                    forSigning: false,
                    data: data,
                    signData: ciphers,
                    signDataType: 'hex',
                    contentType: 'hex',
                    resultType: 'hex'
                }, (e) => {
                    if(e.ok) {
                        this.verifyBuf = '验签成功';
                    }else {
                        this.verifyBuf = '验签失败';
                    }
                });
            }
        }
    }
</script>

<style scoped>
    .wrapper {
        background-color: white;
    }
    .title_root {
        flex-direction: row;
        align-items: center;
        padding-left: 40px;
        padding-right: 40px;
    }
    .tdot {
        width: 20px;
        height: 20px;
        background-color: #0088fb;
        border-radius: 10px;
    }
    .tlab {
        font-size: 32px;
        font-weight: bold;
        margin-left: 20px;
    }
    .pannel {
        flex-direction: column;
        margin-top: 20px;
        margin-bottom: 20px;
        background-color: #F2F2F2;
        border-radius: 10px;
        padding: 40px;
        margin-left: 40px;
        margin-right: 40px;
    }
    .content {
        font-size: 26px;
        color: #666;
    }
</style>