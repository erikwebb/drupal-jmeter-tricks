task default: %w[run]

system("which jmeter > /dev/null 2>&1")
if $?.exitstatus > 0
  $stderr.puts "Unable to find JMeter executable file in \$PATH."
  exit 1
end

desc "Open JMeter script for editing."
task :edit do
  sh "jmeter -p jmeter.properties -t drupal-jmeter-tricks.jmx"
end

desc "Run JMeter script and save results."
task :run do
  sh "jmeter -p jmeter.properties -n -t drupal-jmeter-tricks.jmx -l results.jtl"
end

desc "Perform log analysis on JMeter results."
task :analyze do
  if File.exist?("results.jtl")
    $stdout.puts "Currently unsupported. See http://wiki.apache.org/jmeter/LogAnalysis for examples of log analysis."
  else
    $stderr.puts "Unable to find results.jtl file."
    exit 1
  end
end
