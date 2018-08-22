#!/usr/bin/perl

use strict;
use Digest::SHA qw(hmac_sha1 hmac_sha1_hex);

my $key="8544E3B47ECA58F9583043F8";
my $mac=$ARGV[0];

die "Usage: supermicro-ipmi-key <MAC>" unless $mac;

sub calculate_key {
  my ($data, $key) = map pack('H*', $_), @_;
  hmac_sha1_hex($data, $key);
}

if ($mac =~ /^([\da-zA-z][\da-zA-z]:){5}[\da-zA-z][\da-zA-z]$/ ){
  $mac =~ s/://g;
  my $license_key = substr(calculate_key($mac, $key), 0, 24);
  for (my $i=0; $i<24; $i+=4){
    print substr($license_key, $i, 4)." ";
  }
  print "\n";
} else {
  print "Invalid mac address: $mac\n";
}
