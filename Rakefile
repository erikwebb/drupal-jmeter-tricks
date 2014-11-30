require 'rubygems'
require 'json'
require 'csv'

task default: %w[run]

jmx_file = "test.jmx"
json_file = "results.json"
log_file = "jmeter.log"
properties_file = "jmeter.properties"
results_file = "results.jtl"

system("which jmeter > /dev/null 2>&1")
if $?.exitstatus > 0
  $stderr.puts "Unable to find JMeter executable file in \$PATH."
  exit 1
end

desc "Open JMeter script for editing."
task :edit do
  sh "jmeter -p #{properties_file} -t #{jmx_file}"
end

desc "Run JMeter script and save results."
task :run do
  sh "jmeter -p #{properties_file} -n -t #{jmx_file} -l #{results_file}"
end

desc "Remove current log and results files."
task :clean do
  [json_file, log_file, results_file].each do |file|
    if File.exist?(file)
      File.delete(file)
    end
  end
end

desc "Perform log analysis on JMeter results."
task :analyze do
  if File.exist?(results_file)
    $stdout.puts "Currently unsupported. See http://wiki.apache.org/jmeter/LogAnalysis for examples of log analysis."
  else
    $stderr.puts "Unable to find #{results_file} file."
    exit 1
  end
end

desc "Save the #{results_file} file as JSON."
task :json do
  # Borrowed from http://jasonheppler.org/2014/07/12/parsing-csv-to-json/
  def is_int(str)
    # Check if a string should be an integer
    return !!(str =~ /^[-+]?[1-9]([0-9]*)?$/)
  end

  lines = CSV.read(results_file, {:col_sep => "|"})
  keys = lines.delete lines.first

  File.open(json_file, "w") do |f|
    data = lines.map do |values|
      is_int(values) ? values.to_i : values.to_s
      Hash[keys.zip(values)]
    end
  f.puts JSON.pretty_generate(data)
  end
end
