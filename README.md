const request = require('request');
const logger = require(__dirname + '/assets/sender.js');
const fs = require('fs');
const figlet = require('figlet');
const colors = require('colors');
const readline = require('readline');
var config = require('./config.json');
const triesPerSecond = config['triesPerSecond'];
var working = [];
getGiftCode = function() {
    let _0x8578xa = '';
    let _0x8578xb = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
    for (var _0x8578xc = 0; _0x8578xc < 16; _0x8578xc++) {
        _0x8578xa = _0x8578xa + _0x8578xb['charAt'](Math['floor'](Math['random']() * _0x8578xb['length']))
    };
    return _0x8578xa
};
checkCode = function(_0x8578xa) {
    request(('https://discordapp.com/api/v6/entitlements/gift-codes/' + _0x8578xa + '?with_application=false&with_subscription_plan=true'), (_0x8578xd, _0x8578xe, _0x8578xf) => {
        if (_0x8578xd) {
            logger['error']('An error occurred:');
            logger['error'](_0x8578xd);
            return
        };
        try {
            _0x8578xf = JSON['parse'](_0x8578xf);
            if (_0x8578xf['message'] != 'Unknown Gift Code' && _0x8578xf['message'] != 'You are being rate limited.') {
                logger['info'](('nextu.xyz | https://discord.gift/' + _0x8578xa + ' | Valid'));
                working['push'](('DNCracker by xNextu | https://discord.gift/' + _0x8578xa + ' | nextu.xyz'));
                fs['writeFileSync']('valid-nitros.json', JSON['stringify'](working, null, 4))
            } else {
                logger['info'](('nextu.xyz | ' + _0x8578xa + ' | Invalid'))
            }
        } catch (_0x8578xd) {
            logger['error']('An error occurred:');
            logger['error'](_0x8578xd);
            return
        }
    })
};
console['log'](figlet['textSync']('DNCracker v2.0  |  Nitro')['red']);
console['log'](' ');
console['log'](' ');
console['log']('DNCracker v2.0 | Created by xNextu | nextu.xyz' ['cyan']);
console['log'](' ');
console['log']('Our discord: https://discord.gg/jUfvAzR' ['cyan']);
console['log'](' ');
console['log']('Nitro-Checker started!' ['cyan']);
console['log'](' ');
checkCode(getGiftCode());
setInterval(() => {
    checkCode(getGiftCode())
}, (1 / triesPerSecond) * 1000)

