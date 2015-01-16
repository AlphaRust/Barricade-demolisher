PLUGIN.Title = "Barricade demolisher."
PLUGIN.Description = "Removes every barricade on the map."
PLUGIN.Author = "James Fisher"
PLUGIN.Version = "1"

local dateTime = util.GetStaticPropertyGetter( System.DateTime, 'Now' )
function PLUGIN:Init()
print( self.Title .. " v" .. self.Version .. " Loading..." )

	UseExitReason = new( cs.gettype( "UseExitReason, Assembly-CSharp" ) )

	oxmin_plugin = plugins.Find("oxmin")
	if ( not oxmin_plugin ) then
		self.oxmin = false
	else
		self.oxmin = true
		self.FLAG_canSacks = oxmin.AddFlag("canSacks")
		print( self.Title .. ": canSacks oxmin flag successfully added!")
	end

	self:loadSettings()
	if not self.Settings then return end
	self:loadStats()
	
	self:AddChatCommand( "sacks", self.cmdBarricade )
	
	self.LastRunTime = false
	
	if self.Settings.Timer > 0 then
		self:startTimer()
	end

print( self.Title .. " v" .. self.Version .. " Loaded." )
end

if not self.Timer then
		self.Timer = timer.Repeat( self.Settings.Timer , function() self:clearWood Barricade( true, 0, nil ) end )
	else
		print( self.Title .. ": startTimer, Unable to stop the timer, something is wrong." )
	end
end
		end
	end
	
	self:saveStats()
end
