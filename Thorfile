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
        text = "// Generated from the keyword(s): #{keywords.join(" ")}\n" + comment = "// Title: " + entry["title"] + "\n" + "// User: " + entry["userName"] + "\n" + "// Permutation:" + i.to_s + "\n"

        p.each_with_index do |color,index|
          text << ("$generated-color-#{index+1}: #" + color + ";" "\n")
        end
        puts
        create_file "_generated-colors.scss", text, force: true, verbose: false
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
