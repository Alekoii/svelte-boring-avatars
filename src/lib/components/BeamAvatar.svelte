<script>
	function hashCode(name) {
		let hash = 0;
		for (let i = 0; i < name.length; i++) {
			const character = name.charCodeAt(i);
			hash = (hash << 5) - hash + character;
			hash = hash & hash;
		}
		return Math.abs(hash);
	}

	function getUnit(number, range, index = 0) {
		const value = number % range;
		if (index > 0) {
			return getUnit(Math.floor(number / 10), range);
		}
		return value;
	}

	function getRandomColor(number, colors, range) {
		return colors[number % range];
	}

	function getContrast(hex) {
		const r = parseInt(hex.substr(1, 2), 16);
		const g = parseInt(hex.substr(3, 2), 16);
		const b = parseInt(hex.substr(5, 2), 16);
		const yiq = (r * 299 + g * 587 + b * 114) / 1000;
		return yiq >= 128 ? '#000000' : '#FFFFFF';
	}

	function getBoolean(number, index) {
		return !!(number & (2 ** index));
	}

	let {
		name = 'Biricato',
		colors = ['#fe4365', '#fc9d9a', '#f9cdad', '#c8c8a9', '#83af9b'],
		size = 36,
		square = false,
		title = undefined
	} = $props();

	const SIZE = 36;

	let data = $state({
		wrapperColor: colors[0],
		faceColor: '#FFFFFF',
		backgroundColor: colors[1],
		wrapperTranslateX: 0,
		wrapperTranslateY: 0,
		wrapperRotate: 0,
		wrapperScale: 1,
		isMouthOpen: false,
		isCircle: false,
		eyeSpread: 0,
		mouthSpread: 0,
		faceRotate: 0,
		faceTranslateX: 0,
		faceTranslateY: 0
	});

	function generateData() {
		const numFromName = hashCode(name);
		const range = colors?.length;
		const wrapperColor = getRandomColor(numFromName, colors, range);
		const preTranslateX = getUnit(numFromName, 10, 1);
		const wrapperTranslateX = preTranslateX < 5 ? preTranslateX + SIZE / 9 : preTranslateX;
		const preTranslateY = getUnit(numFromName, 10, 2);
		const wrapperTranslateY = preTranslateY < 5 ? preTranslateY + SIZE / 9 : preTranslateY;

		return {
			wrapperColor,
			faceColor: getContrast(wrapperColor),
			backgroundColor: getRandomColor(numFromName + 13, colors, range),
			wrapperTranslateX,
			wrapperTranslateY,
			wrapperRotate: getUnit(numFromName, 360),
			wrapperScale: 1 + getUnit(numFromName, SIZE / 12) / 10,
			isMouthOpen: getBoolean(numFromName, 2),
			isCircle: getBoolean(numFromName, 1),
			eyeSpread: getUnit(numFromName, 5),
			mouthSpread: getUnit(numFromName, 3),
			faceRotate: getUnit(numFromName, 10, 3),
			faceTranslateX:
				wrapperTranslateX > SIZE / 6 ? wrapperTranslateX / 2 : getUnit(numFromName, 8, 1),
			faceTranslateY:
				wrapperTranslateY > SIZE / 6 ? wrapperTranslateY / 2 : getUnit(numFromName, 7, 2)
		};
	}

	$effect(() => {
		data = generateData();
	});

	const maskId = crypto.randomUUID();
</script>

<svg
	viewBox="0 0 {SIZE} {SIZE}"
	fill="none"
	role="img"
	xmlns="http://www.w3.org/2000/svg"
	width={size}
	height={size}
>
	{#if title}
		<title>{name}</title>
	{/if}

	<mask id={maskId} maskUnits="userSpaceOnUse" x={0} y={0} width={SIZE} height={SIZE}>
		<rect width={SIZE} height={SIZE} rx={square ? undefined : SIZE * 2} fill="#FFFFFF" />
	</mask>

	<g mask={`url(#${maskId})`}>
		<rect width={SIZE} height={SIZE} fill={data.backgroundColor} />
		<rect
			x="0"
			y="0"
			width={SIZE}
			height={SIZE}
			transform={`translate(${data.wrapperTranslateX} ${data.wrapperTranslateY}) 
                   rotate(${data.wrapperRotate} ${SIZE / 2} ${SIZE / 2}) 
                   scale(${data.wrapperScale})`}
			fill={data.wrapperColor}
			rx={data.isCircle ? SIZE : SIZE / 6}
		/>
		<g
			transform={`translate(${data.faceTranslateX} ${data.faceTranslateY}) 
                   rotate(${data.faceRotate} ${SIZE / 2} ${SIZE / 2})`}
		>
			{#if data.isMouthOpen}
				<path
					d={`M15 ${19 + data.mouthSpread}c2 1 4 1 6 0`}
					stroke={data.faceColor}
					fill="none"
					stroke-linecap="round"
				/>
			{:else}
				<path d={`M13,${19 + data.mouthSpread} a1,0.75 0 0,0 10,0`} fill={data.faceColor} />
			{/if}

			<rect
				x={14 - data.eyeSpread}
				y={14}
				width={1.5}
				height={2}
				rx={1}
				stroke="none"
				fill={data.faceColor}
			/>
			<rect
				x={20 + data.eyeSpread}
				y={14}
				width={1.5}
				height={2}
				rx={1}
				stroke="none"
				fill={data.faceColor}
			/>
		</g>
	</g>
</svg>
