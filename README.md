# Omi-trunkspace
Enhance your QBCore server's vehicle experience with a customizable trunk inventory system tailored for specific vehicle models.

1. **Set Up the Custom Trunks Configuration**:
   Start by defining your `Config.CustomTrunks` table with the custom configurations for specific vehicle models in qb-inventory/config.lua:

    ```lua
    Config.CustomTrunks = {
        ['neon'] = { maxweight = 50000, slots = 50 }
        -- Add more custom configurations for other vehicles here
    }
    ```
2. **Search for** ```lua if CurrentVehicle then -- Trunk ``` **in qb-inventory/client/main.lua**
   Replace that whole logic with
    
    ```lua
     if CurrentVehicle then -- Trunk
                local model = GetEntityModel(curVeh)
                local vehicleName = GetDisplayNameFromVehicleModel(model):lower()
                local maxweight, slots
                if Config.CustomTrunks[vehicleName] then
                    maxweight = Config.CustomTrunks[vehicleName].maxweight
                    slots = Config.CustomTrunks[vehicleName].slots
                else
                    if vehicleClass == 0 then
                        maxweight = 38000
                        slots = 30
                    elseif vehicleClass == 1 then
                        maxweight = 50000
                        slots = 40
                    elseif vehicleClass == 2 then
                        maxweight = 75000
                        slots = 50
                    elseif vehicleClass == 3 then
                        maxweight = 42000
                        slots = 35
                    elseif vehicleClass == 4 then
                        maxweight = 38000
                        slots = 30
                    elseif vehicleClass == 5 then
                        maxweight = 30000
                        slots = 25
                    elseif vehicleClass == 6 then
                        maxweight = 30000
                        slots = 25
                    elseif vehicleClass == 7 then
                        maxweight = 30000
                        slots = 25
                    elseif vehicleClass == 8 then
                        maxweight = 15000
                        slots = 15
                    elseif vehicleClass == 9 then
                        maxweight = 60000
                        slots = 35
                    elseif vehicleClass == 12 then
                        maxweight = 120000
                        slots = 35
                    elseif vehicleClass == 13 then
                        maxweight = 0
                        slots = 0
                    elseif vehicleClass == 14 then
                        maxweight = 120000
                        slots = 50
                    elseif vehicleClass == 15 then
                        maxweight = 120000
                        slots = 50
                    elseif vehicleClass == 16 then
                        maxweight = 120000
                        slots = 50
                    else
                        maxweight = 60000
                        slots = 35
                    end
                end
                local other = {
                    maxweight = maxweight,
                    slots = slots,
                }
                TriggerServerEvent("inventory:server:OpenInventory", "trunk", CurrentVehicle, other)
                OpenTrunk()
            elseif CurrentGlovebox then
        ```
    

