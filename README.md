#singleInstance, force
#Persistent
;SplashTextOn, 300, 30, 
jumpJet = 0
;0 = default jump jet
;1 = drifter jet
 
fireMode = 0
;0 = off
;1 = no recoil for auto weps
;2 = full auto for semi auto weps

fireShield = 0
;1 = fire and shield
;0 = off
 
fireQ = 0
;1 = fire and press q
;0 = off
 
burst = 0
;0 = using the fireMode
;1 = overwrite fireMode to burst

vrecoilMult = 1
;recoil multiplier 1 to 3
 
hrecoilMult = 1
;recoil multiplier 1 to 3
 
;hrecoilDir = 2
 
noSpread = 0
 
glitchMoveNum = 0
 
stopLThread = 0
 
wepType = 1
;1 = smg
;2 = carbine/rifles
;3 = shotgun
;4 = sniper rifle
 
CoordMode, Mouse, Relative
CoordMode, Pixel, Relative
 
;Gui, AltSubmit
Gui, Show, w300 h550, Planetside 2 Tool by RiseKAOS
;Gui, Add, Text, x10 y10 w290 Left, RCtrl -- reset and open this window, press it when game starts
Gui, Add, Text, x10 y10 w290 Left, LCtrl+LAlt -- toggle hacks that affect the mouse on/off
Gui, Add, Text, x10 y30 w290 Left, Tab -- burst fire for automatics
Gui, Add, Text, x10 y50 w290 Left, RAlt -- toggle between jump jet and drifter jet
Gui, Add, GroupBox, x10 y130 w200 h100, Weapon Type
Gui, Add, Radio, x20 y150 vWeaponType Checked, SMG (up)
Gui, Add, Radio,, Carbine/Rifles (up and sideways)
Gui, Add, Radio,, Shotgun/Semi-Autos/Pistol (full auto and up)
Gui, Add, Radio,, Sniper Rifles (full auto and up)
Gui, Add, GroupBox, x10 y250 w200 h250, Options
Gui, Add, CheckBox, x20 y270 vFireShield, Shield/Heal on Fire 
Gui, Add, CheckBox, x20 y290 vFireQ, Press Q on Fire
Gui, Add, CheckBox, x20 y310 vNoSpread, No Spread
Gui, Add, CheckBox, x20 y330 vGlitchMove, Glitch Move on Fire
Gui, Add, Text, w290 Left, Vertical Recoil
Gui, Add, DropDownList, vVRecoilMult AltSubmit Choose3, x0|x0.5|x1|x1.5|x2|x2.5|x3|x3.5
Gui, Add, Text, w290 Left, Horizontal Recoil
Gui, Add, DropDownList, vHRecoilMult AltSubmit Choose3, x0|x0.5|x1|x1.5|x2|x2.5|x3|x3.5
;Gui, Add, Text, x20 y450 w290 Left, Horizontal Recoil
Gui, Add, Radio, x150 y420 vHRecoilDir, Left
Gui, Add, Radio, Checked, Right
;Gui, Add, Radio, x30 y330 vRecoilMult, x0
;Gui, Add, Radio,, x0.5
;Gui, Add, Radio, Checked, x1
;Gui, Add, Radio,, x1.5
;Gui, Add, Radio,, x2
;Gui, Add, Radio,, x2.5
;Gui, Add, Radio,, x3
;Gui, Add, Radio,, x3.5
Gui, Add, Button, x210 y520 w80 h20 vUPDATEBUTTON gUPDATE, Update
 
^+x::ExitApp
 
#IfWinActive ahk_class Planetside2 PlayClient (Stage) x64
#NoEnv
;SendMode Input
 
;RCtrl::
 
;Gui, Destroy
;fireMode = 0
;jumpJet = 0
;melee = 0
;burst = 0
;wepType = 1
 
;Gui, Show, w300 h300, Herp Derp
;Gui, Add, Text, x10 y10 w290 Left, RCtrl -- reset and open this window, press it when game starts
;Gui, Add, Text, x10 y30 w290 Left, LCtrl+LAlt -- toggle between none and no recoil
;Gui, Add, Text, x10 y50 w290 Left, Tab -- burst fire for automatics
;Gui, Add, Text, x10 y70 w290 Left, RAlt -- toggle between jump jet and drifter jet
;Gui, Add, Text, x10 y90 w290 Left, Middle mouse button held down -- knife spam
;Gui, Add, Text, x10 y120 w290 Left, Weapon Type:
;Gui, Add, Radio, vWeaponType Checked, SMG
;Gui, Add, Radio,, Carbine/Rifles
;Gui, Add, Radio,, Shotgun
;Gui, Add, Radio,, Sniper Rifles
;Gui, Add, Button, x210 y270 w80 h20 vUPDATEBUTTON gUPDATE, Update
 
;return
 
UPDATE:
 
	Gui, Submit, NoHide
	wepType := WeaponType
	fireShield := FireShield
	noSpread := NoSpread
	if(GlitchMove == 1)
		vrecoilMult := (VRecoilMult - 1) / 2 * (fireQ == 0 ? 6 : 3.5)
	else
		vrecoilMult := (VRecoilMult - 1) / 2
	if(HRecoilDir == 1){
		if(GlitchMove == 1)
			hrecoilMult := -((HRecoilMult - 1) / 2 * (fireQ == 0 ? 4 : 1.5))
		else
			hrecoilMult := -((HRecoilMult - 1) / 2)
	}else if(HRecoilDir == 2){
		if(GlitchMove == 1)
			hrecoilMult := (HRecoilMult - 1) / 2 * (fireQ == 0 ? 4 : 1.5)
		else
			hrecoilMult := (HRecoilMult - 1) / 2
	}
 
return
 
+z::
	
	aimbot += 1
	if(aimbot > 1){
		aimbot = 0
		;terminateAimbot = 1
	}
	
Return
 
LCtrl & LAlt::
 
fireMode += 1
if(fireMode > 1)
   fireMode = 0
 
;ToolTip
;if(fireMode == 0){
;    ToolTip, 0   Off, 100, 100
;}else if(fireMode == 1){
;    ToolTip, 1   No recoil for autos, 100, 100
;}else if(fireMode == 2){
;    ToolTip, 2   Full auto for semi autos, 100, 100
;}else if(fireMode == 3){
;    ToolTip, 3   3x burst, 100, 100
;}
 
return
 
*tab::
 
burst += 1
if(burst > 1)
	burst = 0
 
return
 
*Space::
 
if(jumpJet == 1){
	While GetKeyState("Space", "P"){
		Send {Space Down}
		Sleep 250
		Send {Space Up}
		Sleep 50
	}
}else if(jumpJet == 0){
	Send {Space Down}
	KeyWait, Space
	Send {Space Up}
}	
 
return
 
*RAlt::
 
jumpJet += 1
if(jumpJet > 1)
	jumpJet = 0
 
return
 
*~$MButton::
 
    SetTimer, ButtonHeld, 200
 
return
 
*~$Mbutton up::
 
    SetTimer, ButtonHeld, Off
 
return
 
ButtonHeld:
 
	melee = 1
 
return
 
*~WheelUp::
 
	melee = 0;
 
return
 
*~WheelDown::
 
	melee = 0
 
return
 
*$LButton::
	
	;if(aimbot == 1){
	;	terminateBot = 0
	;	SetTimer, AimBot, 30
	;}
	;if(aimbot == 1){
	;	SetTimer, AimBot, 30
	;	;terminateBot = 0
	;}
	;stopLThread = 0
	;SetTimer, LButtonThread, 100
	
	if(fireShield == 1){
		Send {Space down}
		Sleep 30
		Send {Space up}
	}
	if(fireQ == 1){
		Send {q down}
		Sleep 30
		Send {q up}
	}
    if(melee != 1){
		if(burst == 1){
			Click down
			Sleep 100
			Click up
			Sleep 30
			Click down
			Sleep 100
			Click up
			Sleep 30
			Click down
			Sleep 100
			Click up
			;MouseMove -11, 100, 3, R
			;mouseXY(-1, 6)
		}else{
			if(fireMode == 1 && wepType != 3 && wepType != 4){
				Click down
			}
			if(fireMode == 0){
				Click down
			}
 
			While GetKeyState("LButton", "P"){
				if(aimbot == 1){
					PixelSearch, SpotX, SpotY, 0, 50, 1008, 400, 0xED1C24, 50, FAST RGB
					;ImageSearch, SpotX, SpotY, 0, 0, 1008, 400, %A_ScriptDir%\image4.png
 
					If ErrorLevel
					{
						PixelSearch, SpotX, SpotY, 260, 400, 1000, 700, 0xED1C24, 50, FAST RGB
						
						If ErrorLevel
						{
						}else{
							tempRand = 0
							Random, tempRand, -15, -35
							mouseXY(0, tempRand)
							Sleep 15
							MouseGetPos, NX, NY
							X := SpotX-NX
							Y := SpotY-NY
							Random, tempRand, 50, 80
							mouseXY(0, Y + tempRand)
							Random, tempRand, 10, 35
							mouseXY(X, 0)
						}
					}else{
						tempRand = 0
						Random, tempRand, -15, -35
						mouseXY(0, tempRand)
						Sleep 15
						MouseGetPos, NX, NY
						X := SpotX-NX
						Y := SpotY-NY
						Random, tempRand, 50, 80
						mouseXY(0, Y + tempRand)
						Random, tempRand, 10, 35
						mouseXY(X + tempRand, 0)
					}
				}
 
				if(fireQ == 1 && fireMode != 0){
					Send {q down}
					Sleep 30
					Send {q up}
				}
				if(GlitchMove == 1 && fireMode != 0){
					;if(fireQ == 1){
						Sleep 50
					;}
					if(glitchMoveNum == 0){
						Send {q down}
						Sleep 250
						Send {q up}
						glitchMoveNum = 1
					}else if(glitchMoveNum == 1){
						;Sleep 100
						;Sleep 50
						glitchMoveNum = 2
					}else if(glitchMoveNum == 2){
						Send {d down}
						Sleep 230
						Send {d up}
						glitchMoveNum = 0
					}
				}
				if(noSpread == 1 && fireMode != 0){
					tempRand = 0
					if(GlitchMove == 1){
						Random, tempRand, 1, 21
						mouseXY(tempRand - 11, 0)
					}else{
						Random, tempRand, 1, 5
						mouseXY(tempRand - 3, 0)
					}
					Random, tempRand, 1, 5
					mouseXY(0, tempRand - 3)
				}
				if(wepType != 3 && wepType != 4){
					if(fireMode == 0){
						;do nothing
						Sleep 30
					}else if(fireMode == 1){
						if(wepType == 1){
							if(fireQ == 0)
								mouseXY(0, 2 * vrecoilMult)
							else
								mouseXY(0, 4 * vrecoilMult)
						}else{
							if(fireQ == 0)
								mouseXY(-3 * hrecoilMult, 2 * vrecoilMult)
							else
								mouseXY(-5 * hrecoilMult, 4 * vrecoilMult)
						}
				 		Sleep 50
					}
				}else if(fireMode != 0){
					Click down
					Sleep 15
					Click up
					if(wepType == 3){
						if(fireQ == 0)
							mouseXY(0, 6 * vrecoilMult)
						else
							mouseXY(0, 8 * vrecoilMult)
					}else if(wepType == 4){
						if(fireQ == 0)
							mouseXY(-1, 14 * vrecoilMult)
						else
							mouseXY(-3, 16 * vrecoilMult)
					}
					Sleep 50
				}
			}
			if(fireMode == 1 && wepType != 3 && wepType != 4){
				Click up
			}
			if(fireMode == 0){
				Click up
			}
		}
    }else{
		While GetKeyState("LButton", "P"){
			Click down
			Sleep 15
			Click up
			Sleep 100
		}
    }
 
	if(fireShield == 1){
		Send {Space down}
		Sleep 30
		Send {Space up}
	}
	
	;SetTimer, LButtonThread, Off
	;stopLThread = 1
	
	;if(aimbot == 1){
	;	terminateBot = 1
	;}
	;if(aimbot == 1){
	;	terminateBot = 1
	;}
return
 
LButtonThread:
 
Loop
{
	if(fireQ == 1){
		Send {q down}
		Sleep 30
		Send {q up}
	}
	if(stopLThread == 1){
		return
	}
}
 
return
 
mouseXY(x, y)
{
    DllCall("mouse_event",uint,1,int,x,int,y,uint,0,int,0)
}
 
GuiClose:
ExitApp
