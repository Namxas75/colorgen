require 'open-uri'
require 'json'
require 'color'
class Color < Thor

  include Thor::Actions
  argument :keywords, :desc => "Array of keywords to fetch a color theme", :type => :array

  desc "palette", "Write a scss color palette"
  def palette
    url = 'http://www.colourlovers.com/api/palettes?keywords='+ keywords.join('+').downcase + '&format=json&orderCol=numViews&sortBy=DESC'

    json = JSON.parse(open(url).read)
    palettes = []
    input = ""
    say(" < Enter > requests a new theme, < p + Enter > to get next permutation, < q > to quit:")
    
    json.each do |entry|
      
      entry["colors"].permutation.each_with_index do |p,i|
        named_colors =  "// Generated from the keyword(s): #{keywords.join(" ")}\n" + comment = "// Title: " + entry["title"] + "\n" + "// User: " + entry["userName"] + "\n" + "// Permutation:" + i.to_s + "\n"
        
        text =""
        color_base_url = 'http://www.colourlovers.com/api/color/'

        p.each_with_index do |color,index|
          color_url = color_base_url + color + '&format=json'
          color_data = JSON.parse(open(color_url).read)
          color_name = '$' + color_data[0]['title'].downcase.gsub(/\W/,'')


          named_colors << ("#{color_name}: #" + color + ";" "\n")
          text << ("$generated-color-#{index+1}: " + color_name + ";" "\n")
        end
        puts
        create_file "_generated-colors.scss", named_colors + text, force: true, verbose: false
        case ask("#{entry['title'].capitalize} by #{entry['userName'].capitalize}, permutation: " + i.to_s)
        when "q"
          return
        when ""
          break         
        else
        end
      end
    end
  end
end
