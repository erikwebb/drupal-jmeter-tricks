task default: %w[run]

system("which jmeter > /dev/null 2>&1")
if $?.exitstatus > 0
  $stderr.puts "Unable to find JMeter executable file in \$PATH."
  exit 1
end

task :edit do
  sh "jmeter -p jmeter.properties -t drupal-jmeter-tricks.jmx"
end

task :run do
  sh "jmeter -p jmeter.properties -n -t drupal-jmeter-tricks.jmx -l results.jtl"
end
