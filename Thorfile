require 'open-uri'
require 'json'
require 'color'

class Color < Thor
  include Thor::Actions
  include Object::Color
  argument :keywords, :desc => "Array of keywords to fetch a color theme", :type => :array

  desc "palette", "Write a scss color palette"
  def palette
    combine_words = keywords.join('+').downcase
    url = 'http://www.colourlovers.com/api/palettes?keywords='+ keywords.join('+').downcase + '&format=json&orderCol=numViews&sortBy=DESC'
    # puts url
    page =open(url).read
    json = JSON.parse(page)
    palettes = []

    # p json.first
    input = ""
    puts "\n< Enter > for more palettes from the same keyword(s)  - < s > to stop:"
    puts
    json.each do |entry|

      puts "Title: " + entry["title"]
      puts "User: " + entry["userName"]
      puts
      puts "Resultant SCSS-file:"
      puts
      text = "// Colors from dark to bright\n// Generated from the keyword(s): #{combine_words}\n"
      
      p = sort_color_array entry["colors"]
      p.each_with_index do |color,index|
        name = combine_words.downcase.gsub(/\W+/,"")
        text << ("$generated-color-#{index+1}: #" + color + ";" "\n")
      end
      puts text
      puts
      create_file "_color-constants.scss", text, force: true

      if ask("") == "s"
        break
      end
      
    end
  end



  no_commands do
    def sort_color_array color_array
      h = Hash[ *color_array.collect { |c| [ Color::RGB.by_hex(c).brightness, c ] }.flatten ]
      h.sort.map{|c| c[1]}
    end
  end

end
