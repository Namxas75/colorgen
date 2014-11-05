require 'open-uri'
require 'json'

class Color < Thor
  include Thor::Actions
  argument :keywords, :desc => "an array argument", :type => :array

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
      text = "// Generated from the keyword(s): #{combine_words}\n"
      p = entry["colors"]
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
end
