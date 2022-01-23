# qbcore-old-html
Old qbcore notify HTML 
(You will need to replace this in your qbcore/client/functions.lua

And look for the following code.)

RegisterNUICallback('getNotifyConfig', function(_, cb)
    cb(QBCore.Config.Notify)
end)

function QBCore.Functions.Notify(text, textype, length)
    if type(text) == "table" then
        local ttext = text.text or 'Placeholder'
        local caption = text.caption or 'Placeholder'
        local ttype = textype or 'primary'
        local length = length or 5000
        SendNUIMessage({
            action = 'notify',
            type = ttype,
            length = length,
            text = ttext,
            caption = caption
        })
    else
        local ttype = textype or 'primary'
        local length = length or 5000
        SendNUIMessage({
            action = 'notify',
            type = ttype,
            length = length,
            text = text
        })
    end
end 

(And replace it with the following.)

RegisterNUICallback('getNotifyConfig', function(_, cb)
    cb(QBCore.Config.Notify)
end)

QBCore.Functions.Notify = function(text, textype, length)
    local ttype = textype ~= nil and textype or "primary"
    local length = length ~= nil and length or 5000
    SendNUIMessage({
        action = "show",
        type = ttype,
        length = length,
        text = text,
    })
end
