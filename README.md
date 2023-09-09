how to add it :

one go to qb-apartments client/main.lua

and go to this event 'apartments:client:setupSpawnUI'

and replace it ALL with this

RegisterNetEvent('apartments:client:setupSpawnUI', function(cData)
    QBCore.Functions.TriggerCallback('apartments:GetOwnedApartment', function(result)
        if result then
            TriggerEvent('qb-spawn:client:setupSpawns', cData, false, nil)
            TriggerEvent("apartments:client:SetHomeBlip", result.type)
        else
            if Apartments.Starting then
                TriggerEvent('qb-spawn:client:setupSpawns', cData, true, Apartments.Locations)
                TriggerEvent('qb-spawn:client:openUI', true)
            else
                TriggerEvent('qb-spawn:client:setupSpawns', cData, false, nil)
                TriggerEvent('qb-spawn:client:openUI', true)
            end
        end
    end, cData.citizenid)
end)
two go to qb-spawn client

and go to this event 'qb-spawn:client:setupSpawns'

and replace it ALL with tihs

RegisterNetEvent('qb-spawn:client:setupSpawns', function(cData, new, apps)
    if not new then
        SetNuiFocus(false, false)
        SendNUIMessage({
            type = "ui",
            status = false
        })
        choosingSpawn = false
        Wait(500)
        TriggerEvent("qb-spawnselector:opennui")
    elseif new then
        SendNUIMessage({
            action = "setupAppartements",
            locations = apps,
        })
    end
end)
