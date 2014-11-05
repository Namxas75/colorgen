require 'open-uri'
require 'json'
require 'color'

class Color < Thor
  include Thor::Actions
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
    puts "\n< Enter > for more palettes from the same keyword(s)  - < q > to stop:"
    puts
    json.each do |entry|

      p = entry["colors"]

      name = combine_words.downcase.gsub(/\W+/,"")

      p.permutation.each do |p|

      puts "Title: " + entry["title"]
      puts "User: " + entry["userName"]
      puts
      puts "Resultant SCSS-file:"
      puts
      text = "// Generated from the keyword(s): #{combine_words}\n"
      
        p p
        p.each_with_index do |color,index|
          text << ("$generated-color-#{index+1}: #" + color + ";" "\n")
        end
        puts text
        puts
        create_file "_color-constants.scss", text, force: true
        if ask("< Enter > for next permutation, < q + Enter > for next theme:") == "q"
          break
        end
      end

      if ask("< q > to quit") == "q"
        break
      end
    end
  end
end
