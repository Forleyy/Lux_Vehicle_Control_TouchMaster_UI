<img>https://i.imgur.com/GSGg6DA.jpeg</img>


Hello !

I'll explain you how to plugins_installed

If you have any problem with the UI, contact me via discord : @Forley#8685

If you have problem with the script : https://discord.gg/WBmCPCNdk5


DISCLAMER : IM NOT THE CREATOR OF THE SCRIPT BUT OF THE UI

Original script needed for ui work  : https://github.com/TrevorBarns/luxart-vehicle-control




So let's go install it !


First choose if you want the background with or withtout  the fictive "Lock" text. With by default.

Now just Save the the old "UI" folder, and replace it with the mine.

If you want see all feature work

Replace the Util/cl_lvc.lua with mine OR Read this for put the code needed to the right place (Very Easy)


-- Go to the line 118
-- And place after :
while park_kill or park_kill_masterswitch do

--This code
<code>
while park_kill ~= nil do
       HUD:SetItemState("rls", park_kill)
       Citizen.Wait(1000)
     end
</code>
 -- Now go to the line 241 and search for
<code>
if ( state_lxsiren[veh] ~= proposed_tone or state_lxsiren[veh] == 0 ) then
</code>
--Place this code after..
<code>
  HUD:SetItemState("siren", true)
</code>

-- Now go to the line 244 and search the line
<code>
count_bcast_timer = delay_bcast_timer
else
</code>

-- Add this after else
<code>
if state_pwrcall[veh] == 0 then
    HUD:SetItemState("lft", false)
end
</code>

--Now search for
<code>
HUD:SetItemState("switch", false)  -- Near line 600
</code>
--and add this after
<code>
HUD:SetItemState("lft", false)

</code>







--Now go near the line 660 and search for
<code>
elseif IsDisabledControlJustReleased(0, 172) and not IsMenuOpen() then
  if state_pwrcall[veh] == 0 then
    if IsVehicleSirenOn(veh) then
      PlayAudio("Upgrade", upgrade_volume)
      HUD:SetItemState("siren", true)
      SetPowercallStateForVeh(veh, UTIL:GetToneID('AUX'))
      count_bcast_timer = delay_bcast_timer
    end
  else
    PlayAudio("Downgrade", downgrade_volume)
    if state_lxsiren[veh] == 0 then
      HUD:SetItemState("siren", false)
    end
    SetPowercallStateForVeh(veh, 0)
  end
  SetActivityTimer()
  count_bcast_timer = delay_bcast_timer
end
</code>
And replace with :


<code>
elseif IsDisabledControlJustReleased(0, 172) and not IsMenuOpen() then
  if state_pwrcall[veh] == 0 then
    if IsVehicleSirenOn(veh) then
      PlayAudio("Upgrade", upgrade_volume)
      HUD:SetItemState("lft", true) -- Or Add this
      SetPowercallStateForVeh(veh, UTIL:GetToneID('AUX'))
      count_bcast_timer = delay_bcast_timer
    end
  else
    PlayAudio("Downgrade", downgrade_volume)
    if state_lxsiren[veh] == 0 then
      HUD:SetItemState("siren", false)
        HUD:SetItemState("lft", false) -- And this
    end
    SetPowercallStateForVeh(veh, 0)
  end
  SetActivityTimer()
  count_bcast_timer = delay_bcast_timer
end
</code>



Just after search for



<code>
if state_lxsiren[veh] > 0 then
  if IsDisabledControlJustReleased(0, 80) then
    PlayAudio("Upgrade", upgrade_volume)
    HUD:SetItemState("horn", false)
    SetLxSirenStateForVeh(veh, UTIL:GetNextSirenTone(state_lxsiren[veh], veh, true))
    count_bcast_timer = delay_bcast_timer
  elseif IsDisabledControlPressed(0, 80) then
    HUD:SetItemState("horn", true)
  end
end
</code>



And replace it with

<code>
if state_lxsiren[veh] > 0 then
  if IsDisabledControlJustReleased(0, 80) then
    PlayAudio("Upgrade", upgrade_volume)
  --HUD:SetItemState("horn", false) or Comment this
    HUD:SetItemState("aux2", false) -- And add this
    SetLxSirenStateForVeh(veh, UTIL:GetNextSirenTone(state_lxsiren[veh], veh, true))
    count_bcast_timer = delay_bcast_timer
  elseif IsDisabledControlPressed(0, 80) then
--HUD:SetItemState("horn", true) - And Comment this
    HUD:SetItemState("aux2", true)  -- And add this
  end
end
</ode>






Good job dude !
Now you can play with this nice UI and send me a coffe x)
