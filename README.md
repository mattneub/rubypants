The project from which we are forked (https://github.com/jmcnevin/rubypants) unfortunately uses an early and flawed version of Christian Neukirchen's rubypants. For example, it makes some serious mistakes (as compared to smartypants.pl) with regard to single quotes.

That's not very helpful to users.

So in this fork I have simply replaced rubypants.rb by a more recent version, taken from http://chneukirchen.org/darcs/darcsweb.cgi.

This version _still_ has some flaws (i.e. it does not correctly emulate smartypants). For example:

		require 'rubypants'
		
		def smarty(s)
		  result = nil
		  IO.popen(%{"#{ENV['TM_SUPPORT_PATH']}/bin/SmartyPants.pl"}, "r+") do |io|
			io.write s
			io.close_write
			result = io.read
		  end
		  result
		end
		
		s = "<!-- %br{:clear=>'all'}/ -->"
		
		puts RubyPants.new(s).to_html
		puts smarty(s)
		
		#=> <!-- %br{:clear=>&#8216;all&#8217;}/ &#8211;>
		#=> <!-- %br{:clear=>'all'}/ -->

However, it's better than the earlier version.

