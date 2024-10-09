1. Mealy Machine (Verilog):

module mealy_machine(
	input wire clk,
	input wire reset,
	input wire a,
	output reg y
);

reg [1:0] state;

always @(posedge clk or posedge reset) begin
	if (reset) begin
		state <= 0;
	end else begin
		case (state)
			0: if (a) state <= 1;
			1: if (~a) state <= 0;
			default: state <= 0;
		endcase
	end
end

always @(state) begin
	case (state)
		0: y <= 0;
		1: y <= 1;
		default: y <= 0;
	endcase
end

endmodule


1. Moore Machine (VHDL):

vhdl
library IEEE;
use IEEE.STD_LOGIC;
use IEEE.NUMERIC_STD.ALL;

entity moore_machine is
Port ( clk : in STD_LOGIC;
reset : in STD_LOGIC;
a : in STD_LOGIC;
y : out STD_LOGIC);
end moore_machine;

architecture Behavioral of moore_machine is
type state_type is (S0, S1);
signal state : state_type;
begin
process(clk, reset)
begin
	if (reset = '1') then
		state <= S0;
	elsif (rising_edge(clk)) then
		case state is
			when S0 => if (a = '1') then state <= S1;
			when S1 => if (a = '0') then state <= S0;
			when others => state <= S0;
		end case;
	end if;
end process;

y <= '1' when (state = S1) else '0';

end Behavioral;


Testbench (Verilog):

module testbench;
reg clk, reset, a;
wire y;

mealy_machine uut(
	.clk(clk),
	.reset(reset),
	.a(a),
	.y(y)
);

initial begin
	clk = 0;
	forever #5 clk = ~clk;
end

initial begin
	reset = 1; #10 reset = 0;
end

initial begin
	a = 0; #20 a = 1; #20 a = 0; #20 a = 1;
end

endmodule


Testbench (VHDL):

vhdl
library IEEE;
use IEEE.STD_LOGIC;
use IEEE.NUMERIC_STD.ALL;

entity testbench is
end testbench;

architecture Behavioral of testbench is
component moore_machine
Port ( clk : in STD_LOGIC;
reset : in STD_LOGIC;
a : in STD_LOGIC;
y : out STD_LOGIC);
end component;

signal clk, reset, a, y : STD_LOGIC;

begin
uut: moore_machine
Port map (
	clk => clk,
	reset => reset,
	a => a,
	y => y
);

clock_process : process
begin
	clk <= '0';
	wait for 5 ns;
	clk <= '1';
	wait for 5 ns;
end process;

reset_process : process
begin
	reset <= '1';
	wait for 10 ns;
	reset <= '0';
	wait;
end process;

stim_process : process
begin
	a <= '0';
	wait for 20 ns;
	a <= '1';
	wait for 20 ns;
	a <= '0';
	wait for 20 ns;
	a <= '1';
	wait;
end process;

end Behavioral;
